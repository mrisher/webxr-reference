# questions

Questions for Brandon and other members of the team.

**What does it mean for a WebGL canvas to be compatible with the XRDevice?**

_The Explainer has this paragraph:_ In order for a WebGL canvas to be used with an XRWebGLLayer, its context must be compatible with the XRDevice. This can mean different things for different environments. For example, on a desktop computer this may mean the context must be created against the graphics adapter that the XRDevice is physically plugged into. On most mobile devices though, that's not a concern and so the context will always be compatible. In either case, the WebXR application must take steps to ensure WebGL context compatibility before using it with an XRWebGLLayer.
