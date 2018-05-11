 collection of vertices and materials is known as a model or a mesh

fps: Stands for frames per second. This a measurement of the total amount of consecutive frame redraws done in one-second. The lower this amount, the more poorly your game is performing. You typically want your game to run at 60fps, which will make your game look and feel smooth.
◆: Stands for total draw calls per frame. This is typically the total amount of visible objects drawn per single frame. Lights affecting objects can also increase the amount of draw calls of an object. The lower this amount, the better.
▲: Stands for total polygons per frame. This the total amount of polygons used to draw a single frame for all the visible geometry. The lower this amount, the better.
✸: Stands for total visible light sources. This is the total amount of light sources currently affecting visible objects. The SceneKit guidelines recommend not using more than 3 light sources at a time.

The SceneKit physics simulation uses the International System of Units (SI) for measurements: Kilograms for units of mass, Newtons for units of force, Newton-second for units of impulse, and Newton-meter for units of torque.


Update: The view calls renderer(_: updateAtTime:) on its delegate. This is a good spot to put basic scene update logic.
Execute Actions & Animations: SceneKit executes all actions and performs all attached animations to the nodes in the scene graph.
Did Apply Animations: The view calls its delegate’s renderer(_: didApplyAnimationsAtTime:). At this point, all the nodes in the scene have completed one single frame’s worth of animation, based on the applied actions and animations.
Simulates Physics: SceneKit applies a single step of physics simulation to all the physics bodies in the scene.
Did Simulate Physics: The view calls renderer(_: didSimulatePhysicsAtTime:) on its delegate. At this point, the physics simulation step has completed, and you can add in any logic dependent on the physics applied above.
Evaluates Constraints: SceneKit evaluates and applies constraints, which are rules you can configure to make SceneKit automatically adjust the transformation of a node.
Will Render Scene: The view calls renderer(_: willRenderScene: atTime:) on its delegate. At this point, the view is about to render the scene, so any last minute changes should be performed here.
Renders Scene In View: SceneKit renders the scene in the view.
Did Render Scene: The final step is for the view to call its delegate’s renderer(_: didRenderScene: atTime:). This marks the end of one cycle of the render loop; you can put any game logic in here that needs to execute before the process starts anew.

Command & Option


pb = SCNPhysicsBody(type: .static, shape: SCNPhysicsShape(node: n, options: nil))
SCNLookAtConstraint