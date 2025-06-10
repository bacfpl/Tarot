# Technology Stack cho Web Game Tarot

## 1. Frontend Core
### Unity WebGL
- Unity 2022.3 LTS hoặc mới hơn
- WebGL 2.0 support
- Compression và optimization:
  + Brotli compression
  + Asset bundle optimization
  + Texture compression (DXT/ASTC)
  + Code stripping
  + IL2CPP build

### Web Framework
- Next.js 14 (React Framework)
  + App Router cho performance tối ưu
  + Server Components
  + React Server Components
  + Static Site Generation cho content tĩnh
  + Dynamic imports cho code splitting

### State Management & Real-time
- Zustand cho local state
- SWR cho data fetching
- Socket.IO cho game state synchronization
- WebRTC cho voice communication:
  + Peer-to-peer connection
  + Low latency audio streaming
  + Fallback TURN servers
  + Audio quality optimization

### Real-time Data Flow
```typescript
// Game State Interface
interface GameState {
  sessionId: string;
  readerId: string;
  spreadType: string;
  gamePhase: 'preparation' | 'shuffling' | 'drawing' | 'reading' | 'completed';
  cards: CardState[];
  lastAction: {
    type: 'SHUFFLE' | 'DRAW' | 'PLACE' | 'FLIP' | 'COMPLETE';
    timestamp: number;
  };
}

// Minimal Chat Interface
interface ChatMessage {
  timestamp: number;
  type: 'reader' | 'seeker';
  // Không lưu nội dung chat
}
```

### Graphics & Animation
- Three.js cho 3D effects ngoài game
- GSAP cho web animations
- Canvas API cho 2D effects
- WebGL shaders cho visual effects đặc biệt

## 2. Backend Architecture

### API Layer
- Node.js với Fastify
  + Game state management
  + Session handling
  + Basic authentication
  + Payment processing

### Voice Server
- Mediasoup cho WebRTC SFU
  + Selective Forwarding Unit
  + Bandwidth adaptation
  + Multiple audio qualities
  + Network resilience
- TURN/STUN servers
  + Coturn server deployment
  + Global server distribution
  + Fallback mechanisms
  + NAT traversal

### Real-time Server
- Socket.IO
  + Game state synchronization
  + Voice call signaling
  + Session management
  + Connection handling

### Database & Storage
- MongoDB Atlas
  + Game sessions
  + Reader profiles
  + Transaction records
  + Không lưu trữ chat logs

### Caching Layer (Redis)
- Session data
- Game state
- Rate limiting
- Temporary data

### Game Server (Unity)
- Photon Fusion/Mirror
  + Low latency networking
  + State synchronization
  + Delta compression
  + Interest management

## 3. Database & Caching

### Primary Database
- MongoDB Atlas
  + Sharding cho scalability
  + Replica sets cho high availability
  + Change streams cho real-time updates
  + Time series collections cho analytics

### Caching Layer
- Redis Stack
  + Session storage
  + Real-time leaderboards
  + Pub/Sub system
  + Rate limiting
  + JSON storage
  + Search capability

### Asset Storage
- AWS S3/Cloudfront
  + Global CDN
  + Edge caching
  + Image optimization
  + Video streaming
  + Versioning

## 4. Performance Optimization

### Frontend Optimization
```typescript
// Code splitting example
const GameRoom = dynamic(() => import('@/components/GameRoom'), {
  loading: () => <LoadingSpinner />,
  ssr: false
});

// Preloading assets
const preloadAssets = () => {
  const assets = [
    '/cards/major-arcana/*.webp',
    '/cards/minor-arcana/*.webp',
    '/effects/*.webgl'
  ];
  return Promise.all(assets.map(src => prefetch(src)));
};
```

### WebGL Optimization
```typescript
// WebGL context optimization
const initWebGL = () => {
  const ctx = canvas.getContext('webgl2', {
    alpha: false,
    antialias: false,
    depth: true,
    powerPreference: 'high-performance',
    premultipliedAlpha: false,
    preserveDrawingBuffer: false
  });
};

// Texture loading optimization
const loadTexture = async (url: string) => {
  const response = await fetch(url);
  const blob = await response.blob();
  return createImageBitmap(blob, {
    imageOrientation: 'flipY',
    premultiplyAlpha: 'none'
  });
};
```

### Network Optimization
```typescript
// WebSocket message compression
const compression = {
  threshold: 1024, // bytes
  level: 6, // compression level
  strategy: 'dynamic' // dynamic compression
};

// Binary protocol for card states
interface CardState {
  id: number;      // 2 bytes
  position: {      // 4 bytes
    x: number,     // 2 bytes
    y: number      // 2 bytes
  };
  isReversed: boolean; // 1 bit
  state: number;   // 1 byte
}
```

## 5. Deployment & Scaling

### Infrastructure (AWS)
- ECS Fargate cho containerized services
- ElastiCache cho Redis cluster
- DocumentDB cho MongoDB compatibility
- CloudFront cho global CDN
- Route53 cho DNS management
- WAF cho security

### CI/CD Pipeline
- GitHub Actions
- Docker containers
- Automated testing
- Blue-green deployment
- Canary releases
- Automated rollbacks

### Monitoring
- Datadog
  + APM (Application Performance Monitoring)
  + Real-time metrics
  + Log aggregation
  + Distributed tracing
  + Custom dashboards

## 6. Security Measures

### Network Security
- CloudFlare
  + DDoS protection
  + WAF rules
  + Bot protection
  + SSL/TLS encryption
  + Rate limiting

### Application Security
- JWT với rotating keys
- Rate limiting per user/IP
- Input validation
- XSS protection
- CSRF tokens
- Content Security Policy

## 7. Scaling Strategy

### Horizontal Scaling
- Load balancing với Nginx
- Service discovery với Consul
- Message queue với RabbitMQ
- Stateless architecture
- Database sharding

### Performance Metrics
- Time to First Byte (TTFB) < 200ms
- First Contentful Paint (FCP) < 1s
- Time to Interactive (TTI) < 2s
- WebSocket latency < 100ms
- Frame rate > 60fps 

### Voice Communication System
```typescript
// Voice Call Configuration
interface VoiceConfig {
  audioConstraints: {
    echoCancellation: true,
    noiseSuppression: true,
    autoGainControl: true,
    sampleRate: 48000,
    channelCount: 1
  };
  connectionConfig: {
    iceServers: [
      { urls: 'stun:stun.l.google.com:19302' },
      { urls: 'turn:your-turn-server.com', 
        username: 'username',
        credential: 'credential' 
      }
    ]
  };
}

// Session State Interface
interface SessionState {
  sessionId: string;
  readerId: string;
  seekerId: string;
  gamePhase: 'preparation' | 'shuffling' | 'drawing' | 'reading' | 'completed';
  voiceStatus: {
    connected: boolean;
    muted: boolean;
    speaking: boolean;
    quality: 'good' | 'fair' | 'poor'
  };
  cards: CardState[];
  lastAction: GameAction;
}
```

### Voice Quality Optimization
```typescript
// Audio Processing Pipeline
const initAudioPipeline = () => {
  const audioContext = new AudioContext();
  const audioWorklet = new AudioWorkletNode(audioContext, 'processor');
  
  // Noise reduction
  const denoise = audioContext.createDynamicsCompressor();
  denoise.threshold.value = -50;
  denoise.knee.value = 40;
  denoise.ratio.value = 12;
  
  // Echo cancellation
  const echoCanceller = new EchoCanceller();
  
  // Voice activity detection
  const vad = new VADNode(audioContext);
  
  // Audio quality monitoring
  const analyzer = audioContext.createAnalyser();
  analyzer.fftSize = 2048;
};

// Network Quality Monitoring
interface NetworkStats {
  bitrate: number;
  packetLoss: number;
  latency: number;
  jitter: number;
}

const adjustAudioQuality = (stats: NetworkStats) => {
  if (stats.packetLoss > 0.1 || stats.latency > 150) {
    reduceBitrate();
    enableFEC();
  }
};
```

### Voice Session Management
- Automatic reconnection
- Quality monitoring
- Bandwidth adaptation
- Fallback options:
  + Lower quality audio
  + Temporary text chat
  + Automatic reconnect

## 8. Infrastructure Requirements

### Voice Server Infrastructure
- Dedicated voice servers
- Global server distribution
- Auto-scaling based on load
- Redundancy for reliability

### Network Requirements
- Low latency connections
- High availability
- Bandwidth monitoring
- Quality of Service (QoS)

### Monitoring & Analytics
- Voice quality metrics
- Connection statistics
- User experience data
- Performance monitoring 