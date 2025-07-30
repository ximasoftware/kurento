# DTMF Investigation in Kurento WebRTC Media Server

## Problem Statement
Kurento code doesn't handle DTMF tones properly - it breaks when encountering them instead of treating them differently from regular audio.

## Key Findings

### Codebase Structure
```
/home/bashby/projects/xima/kurento/server/
├── module-core/              # Core media processing logic
│   └── src/
│       ├── gst-plugins/      # GStreamer plugins
│       └── server/
│           └── implementation/objects/
│               ├── BaseRtpEndpointImpl.cpp/hpp  # Base RTP handling
│               ├── SdpEndpointImpl.cpp/hpp      # SDP handling
│               └── MediaElementImpl.cpp/hpp     # Core media element
├── module-elements/          # Specific endpoint implementations
│   └── src/
│       ├── gst-plugins/
│       │   ├── rtpendpoint/          # RTP endpoint GStreamer plugin
│       │   └── webrtcendpoint/       # WebRTC endpoint GStreamer plugin
│       └── server/implementation/objects/
│           ├── RtpEndpointImpl.cpp/hpp     # RTP endpoint implementation
│           └── WebRtcEndpointImpl.cpp/hpp  # WebRTC endpoint implementation
```

### Key Files for RTP Processing (Priority Order)
1. **BaseRtpEndpointImpl.cpp/hpp** - Base class for all RTP endpoints
2. **WebRtcEndpointImpl.cpp/hpp** - WebRTC-specific endpoint implementation
3. **RtpEndpointImpl.cpp/hpp** - Pure RTP endpoint implementation
4. **kmswebrtcendpoint.c/h** - GStreamer WebRTC endpoint plugin
5. **kmsrtpendpoint.c/h** - GStreamer RTP endpoint plugin
6. **kmsrtpsession.c/h** - RTP session management
7. **kmswebrtcsession.c/h** - WebRTC session management

## Investigation Status
- [x] Mapped codebase structure
- [x] Analyzed BaseRtpEndpointImpl for RTP packet handling
- [ ] Analyzed WebRtcEndpointImpl for DTMF-specific logic
- [ ] Examined GStreamer plugin implementations
- [ ] Located RTP packet processing pipelines
- [x] Found DTMF reference in SDP test (telephone-event/8000)
- [ ] Identified DTMF detection/handling points
- [ ] Found where audio processing breaks with DTMF

## Next Steps
1. Read BaseRtpEndpointImpl to understand base RTP handling
2. Look at WebRtcEndpointImpl for WebRTC-specific DTMF logic
3. Examine GStreamer plugins for low-level RTP processing
4. Search for DTMF-related code and configurations
5. Identify where RTP payload type handling occurs
