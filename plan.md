# Kế Hoạch Phát Triển Web Game Tarot Online (Unity WebGL)

## 1. Kiến trúc Hệ thống
- **Game Engine:** Unity (C#) với WebGL build
- **Web Platform:** React.js (cho website wrapper và UI ngoài game)
- **Backend:** ASP.NET Core (cho game server và web API)
- **Database:** MongoDB (lưu thông tin reader và lịch sử reading)
- **Network:** Photon Engine/Mirror (cho multiplayer và real-time communication)
- **Hosting:** Web server cho static content và WebGL build

## 2. Các Tính Năng Chính

### A. Website Features (React)
- Landing page với game introduction
- Reader authentication và account management
- Tarot reading room access cho khách
- Simple lobby system
- Responsive design cho mobile access
- Game embedding system
- Virtual currency management system
- Payment gateway cho readers

### B. Game Features (Unity WebGL)
- Tarot reading room với UI/UX đẹp mắt
- Single reading session system
- Card system với animations
- Basic chat system trong game
- Recording system
- Cross-browser compatibility

### C. Reader Features
- Tạo profile chuyên nghiệp với avatar
- Calendar integration cho lịch làm việc
- Quản lý reading sessions
- Reading room interface với các hiệu ứng đẹp mắt
- Công cụ spread bài tarot với animation
- Text chat với khách
- Quản lý credit/virtual currency
- Theo dõi lịch sử giao dịch

### D. Guest (Seeker) Features
- Truy cập reading room trực tiếp qua link
- Text chat với reader trong session
- Xem bài tarot được bốc
- Basic interaction với cards
- Download/save reading result

### E. Tarot Reading Interface
- Bộ bài Tarot 78 lá với artwork 2D chất lượng cao
- Các spread layout cơ bản (3-card, Celtic Cross)
- Animations cho shuffle, draw, và reveal cards
- Basic particle effects và sound effects
- Screenshot/save reading kết quả
- Mobile-friendly controls

## 3. Kế Hoạch Phát Triển

### Phase 1: MVP (Minimum Viable Product)
- Setup Unity WebGL project
- Basic website framework với React
- Reader authentication system
- Simple tarot interface
- Basic card interaction
- WebGL build và web integration

### Phase 2: Core Features
- Advanced card animations
- Basic reading room functionality
- Text chat system
- Website-game communication
- Reading session recording

### Phase 3: Enhanced Features
- Thêm spread layouts
- Advanced card effects
- Enhanced room features
- Performance improvements
- Mobile optimization

### Phase 4: Future Features (Seeker Account System)
- Seeker registration và authentication
- Profile system cho seekers
- Reading history cho registered seekers
- Rating và review system
- Booking system
- Payment integration
- Social features

## 4. Tech Stack Chi Tiết

### Game Development (Unity)
- Unity 2022.3 LTS với WebGL support
- C# cho game logic
- DOTween cho animations
- Optimized assets cho web loading

### Web Development
- React.js cho website framework
- TypeScript cho type safety
- Tailwind CSS cho styling
- Redux cho state management
- WebGL integration components

### Backend Services
- ASP.NET Core cho game server và web API
- MongoDB cho database
- JWT cho reader authentication
- Redis cho credit caching
- Payment gateway services
- Transaction monitoring system

### Asset Pipeline
- Optimized 2D artwork cho web
- Compressed audio assets
- Sprite atlasing
- Asset bundling và lazy loading
- WebGL compression

### DevOps
- Git cho version control
- CI/CD pipeline cho web deployment
- Docker cho development environment
- AWS/Azure cho hosting
- CDN cho asset delivery

### Payment Integration
- VNPay SDK integration
- Momo Payment SDK
- Stripe cho international payments
- Custom credit management system
- Transaction logging system

## 5. Technical Considerations
- WebGL performance optimization
- Browser compatibility
- Mobile device support
- Asset loading và caching
- Network latency handling
- Memory management
- Basic security measures
- Cross-browser testing
- Progressive loading

## 6. Monetization Model (Future Phase)
- Reader subscription plans
- Premium card designs/effects
- Custom room themes
- Special effects và animations
- Booking fees
- Featured reader listings

## 7. Hệ Thống Credit và Thanh Toán

### Virtual Currency (Credit) System
- 1 Credit = X VND (có thể điều chỉnh tỷ giá)
- Readers phải mua credits để sử dụng platform
- Credits được trừ theo:
  + Số lượng reading sessions hoàn thành
  + Loại spread được sử dụng
  + Các tính năng premium được kích hoạt

### Payment Flow
1. Reader mua credits:
   - Chọn gói credits (ví dụ: 100, 500, 1000 credits)
   - Thanh toán qua các cổng:
     + Momo
     + VNPay
     + Bank Transfer
     + International Cards
   - Credits được cộng vào tài khoản

2. Sử dụng credits:
   - Trừ credits sau khi hoàn thành reading session
   - Thông báo khi credits sắp hết
   - Option để auto-buy credits
   - Không giới hạn thời gian cho mỗi session

3. Pricing Structure
   - Gói Starter: 100 credits = 100,000 VND
   - Gói Basic: 500 credits = 450,000 VND (10% bonus)
   - Gói Pro: 1000 credits = 850,000 VND (15% bonus)
   - Gói Premium: 2000 credits = 1,600,000 VND (20% bonus)

### Credit Usage
- Reading Sessions theo loại spread:
  + 3-Card Spread = 10 credits (60 phút)
  + Celtic Cross = 20 credits (90 phút)
  + Custom Complex Spread = 15-25 credits (75-120 phút)
  + Special/Ritual Spread = 30 credits (120 phút)

- Thời gian session:
  + Mỗi loại spread có thời gian cố định dư dả
  + Timer hiển thị đếm ngược nhẹ nhàng
  + Cảnh báo khi còn 15 phút
  + Tự động kết thúc sau thời gian quy định
  + Option extend thêm 15 phút (miễn phí 1 lần)
  + Có thể kết thúc sớm nếu reading hoàn tất

- Tính năng bổ sung (Optional):
  + Save reading history với ảnh = 2 credits
  + Export detailed reading report = 3 credits
  + Special card effects/animations = 1 credit
  + Custom room themes = 5 credits/theme
  + Extend thêm thời gian (sau lần đầu) = 5 credits/15 phút

- Ưu đãi cho Readers:
  + Giảm 20% credit cost sau 50 readings thành công
  + Giảm 30% credit cost sau 200 readings thành công
  + Nhận 10 credits miễn phí mỗi khi đạt milestone mới
  + Bonus credits cho rating cao (4.5+ sao)
  + Thêm 15 phút miễn phí cho mỗi session khi đạt Pro level

### Reader Benefits
- Thời gian session được tính toán dư dả
- Có thể extend thời gian nếu cần
- Không bị áp lực về tốc độ reading
- Timer chỉ mang tính chất quản lý thời gian
- Được hoàn credits nếu session bị disconnect do lỗi kỹ thuật
- Có thể tặng credits cho regular clients
- Hệ thống loyalty rewards

### Session Management
- Hiển thị thời gian còn lại
- Notification nhẹ nhàng ở các mốc:
  + 30 phút còn lại
  + 15 phút còn lại
  + 5 phút còn lại
- Options khi gần hết giờ:
  + Extend thời gian
  + Kết thúc session
  + Lưu kết quả nhanh
- Auto-save kết quả khi session kết thúc

### Reporting & Analytics
- Dashboard cho readers theo dõi:
  + Credit balance
  + Reading session history
  + Transaction history
  + Revenue analytics
  + Client feedback và ratings
- Admin dashboard:
  + Monitor credit flow
  + Transaction monitoring
  + Revenue reports
  + User behavior analytics
  + Reader performance metrics

### Security & Compliance
- Mã hóa thông tin giao dịch
- Log đầy đủ credit movements
- Backup system cho credit data
- Dispute resolution system
- Anti-fraud measures
- Bảo vệ quyền lợi của reader 