# Streaming

## Streaming thread
The "pt_texture_read_input_stream" consists of two stages. The first stage is a serial stage which is executed by the caller thread due to the limit of the serial slob allocator(TODO: find a parallel alternative) while the second stage is to spawn a TBB task(Technically, this task is not spawned but enqueued to the same task arena to make sure the value returned by "tbb::this_task_arena::current_thread_id" is unique) which uses the "tbb::this_task_arena::current_thread_id" to select the proper "command_pool" and "command_buffer".

## Main rendering thread
The "pt_gfx_connection_draw_acquire" calls the "reduce_streaming_task" which can be considered as the third stage after the second stage of the "pt_texture_read_input_stream". In fact, the whole streaming process can be considered as a "serial-parallel-serial" parallel pipeline since the implemention of the "parallel-serial" part of the parallel pipeline is intrinsically equivalent to the parallel reduce.

## Performance tuning
There are three variables which should be tuning according to the specific project.

### transfer_src_buffer_size
The "transfer_src_buffer_size" is size of the staging buffer of this engine. When there is no enough memory, the spawned TBB task will be pushed into the "streaming_task_respawn_list". If you find the count of the "streaming_task_respawn" is too high, you may increase the size of the "transfer_src_buffer".

### STREAMING_TASK_RESPAWN_LINEAR_LIST_COUNT
The "streaming_task_respawn_list" is a "mp_list" which consists of two parts: a "linear_list" and a "link_list". Ideally, the "link_list" should rarely be used since it's harmful to the performance. If you find the count of the "link_list" is too high , you may increase the value of the "STREAMING_TASK_RESPAWN_LINEAR_LIST_COUNT".

### STREAMING_OBJECT_LINEAR_LIST_COUNT
The "streaming_object_list" contains the objects which have completed the second stage or have been cancelled or in error during the second stage. This list can considered as a "input_item_buffer" between the second stage and the third stage of the parallel pipeline. Evidently, the size of this list will impact the throughput. And this list is a "mp_list" as well. Similarly, you should try to avoid the usage of the "link_list" by increasing the value of the "STREAMING_OBJECT_LINEAR_LIST_COUNT".