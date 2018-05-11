1. Metal encompasses the Metal framework, MetalKit framework, Metal Performance Shaders framework, Metal shading language, and Metal standard library
2. Metal and MetalKit. Metal provides access to the GPU, and MetalKit provides common utilities that make it easier to develop a Metal app
3. a MetalKit view automatically sets up and manages a continuous rendering loop that provides you with a 2D, displayable resource, commonly known as a drawable, for each frame
4. You can use Core Animation directly to develop a Metal app, but it’s easier, faster, and more convenient to use MetalKit.
5. A MTLDevice object represents a GPU
6. a MTLCommandQueue object to create and organize MTLCommandBuffer objects, ensuring that they’re sent to the GPU in the correct order. For every frame, a new MTLCommandBuffer object is created
7. diagram
    1. Command buffers are created from a command queue
    2. Command encoders encode commands into command buffers
    3. Command buffers are then committed and sent to the GPU
    4. The GPU executes the commands and renders the results to a drawable