---
title: "Bilateral teleoperation over network (source code and video)"
pubDate: "2020-01-15T15:09:11.000Z"
description: "A C++ force-feedback teleoperation demo linking two Geomagic Touch devices over a network."
---
It’s been more than a year since I made a post as I’ve been quite busy to be honest. Thankfully, I passed my PhD viva and I’m currently working as a researcher at King’s College London. Currently on my way to come up with a research plan, nevertheless, due to other various tasks I do in parallel, I managed to create some C++ code for bilateral teleoperation, i.e. teleoperation with force feedback using two Geomagic Touch devices by 3DSystems over a network. You can find the [code on Github](https://github.com/constanton/TouchP2P).

The bilateral teleoperation system uses a position – position configuration. This means that the angular values of the joints are only exchanged between the devices. The upside is that there is no need for force sensors and external tools, as required by the position-force configuration, to receive forces from the remote environment. This conveniently keeps the system nice and simple but also more functional as all the moving parts of the robotic arm will respond to any change imposed by the remote environment. The downside is that in terms of transparency (quality of telepresence) during contact it is just not as good as the alternative.

The touchp2p.cpp file once compiled on each PC where the Touch devices are connected, runs a PID controller that receives reference angular values of the joints of the other device. It is only required to **set the correct IPs** of the remote and local machine on each side of the teleoperation system. The code uses the Boost C++ library for the networking and multithreading bits. The library to control these devices, namely OpenHaptics, is not open source but at least for educational purposes I’m allowed to share my code. The math and the relevant code behind the PID controller design are the same for any device of similar type anyway. Here is a video (even though the point is to experience the demo through touch):

<iframe src="https://player.vimeo.com/video/385028514" title="Embedded video" loading="lazy" allow="fullscreen; picture-in-picture; encrypted-media" allowfullscreen></iframe>

**Note**: The PID values in the code are not exactly optimized, so in case you optimize them feel free to share them with me. Also, as always the code is not so clean but it works. Enjoy!

Special thanks to Professor Marcelo A. C. Fernandes as my code is based on previous effort for a similar project.
