# Hệ Thống Tarot

## 1. Bộ Bài Tarot
### Major Arcana (22 lá)
- Đầy đủ 22 lá Major Arcana từ The Fool (0) đến The World (21)
- Mỗi lá có:
  + Hình ảnh chất lượng cao
  + Ý nghĩa cơ bản (Upright & Reversed)
  + Keywords cho quick reading
  + Detailed interpretation guide

### Minor Arcana (56 lá)
- 4 suits (Wands, Cups, Swords, Pentacles)
- Mỗi suit có:
  + Ace to 10
  + Court Cards (Page, Knight, Queen, King)
  + Keywords và meanings cho mỗi lá
  + Elemental associations

## 2. Card Interaction System

### Cơ Chế Shuffle
- Shuffle ảo với animation đẹp mắt
- Random algorithm đảm bảo tính ngẫu nhiên
- Options cho shuffle:
  + Auto shuffle
  + Manual shuffle (kéo thả)
  + Ritual shuffle (3 lần, 7 lần, etc.)
  + Cut deck option

### Card Drawing
- Smooth drawing animation
- Có thể xem preview trước khi lật
- Hiệu ứng lật bài đẹp mắt
- Option để:
  + Draw một lá
  + Draw nhiều lá cùng lúc
  + Reverse cards (tùy chọn)

### Card Placement
- Grid system cho các spread khác nhau
- Snap-to-grid cho vị trí chuẩn xác
- Highlight vị trí cần đặt bài
- Thông tin về ý nghĩa của mỗi vị trí

## 3. Spread Systems

### Basic Spreads
1. **Single Card**
   - Quick daily guidance
   - Yes/No questions
   - Daily energy reading

2. **Three Card Spread**
   - Past-Present-Future
   - Mind-Body-Spirit
   - Situation-Action-Outcome
   - Custom 3-card layouts

3. **Celtic Cross**
   - Full 10-card spread
   - Detailed position meanings
   - Step-by-step guidance
   - Interactive tutorial

### Advanced Spreads
- Relationship Spread
- Career Path Spread
- Monthly Forecast
- Spiritual Journey
- Custom Spreads (cho Pro readers)

## 4. Reading Interface

### Card Information Display
- Card name và số
- Keywords
- Basic meaning
- Detailed interpretation
- Related symbols
- Element associations
- Astrological connections

### Reading Tools
- Zoom vào card details
- Flip between upright/reversed
- Quick meaning reference
- Note-taking system
- Highlight key points
- Save card combinations

### Interpretation Aids
- Keyword suggestions
- Card relationship hints
- Pattern recognition
- Theme identification
- Element/Number patterns
- Spread position reminders

## 5. Special Features

### Card Effects
- Subtle animations
- Energy flow visualization
- Connection lines between cards
- Highlight related cards
- Custom card backs
- Special card frames

### Reading Environment
- Customizable backgrounds
- Ambient sound options
- Mood lighting effects
- Table cloth options
- Special occasion themes
- Ritual elements

### Recording System
- Screenshot functionality
- Reading summary export
- Save interpretations
- Share reading results
- Progress tracking
- Collection system

## 6. Learning System

### Tutorial Mode
- Interactive lessons
- Card meaning guides
- Spread tutorials
- Practice readings
- Feedback system
- Progress tracking

### Reference Library
- Card encyclopedia
- Spread directory
- Symbol dictionary
- Element guide
- Number meanings
- Color associations

### Practice Tools
- AI practice client
- Random scenarios
- Timing exercises
- Interpretation practice
- Pattern recognition drills
- Memory games

## 7. Technical Details

### Card Data Structure
```typescript
interface TarotCard {
  id: number;
  name: string;
  type: 'major' | 'minor';
  suit?: 'wands' | 'cups' | 'swords' | 'pentacles';
  number: number;
  meanings: {
    upright: string[];
    reversed: string[];
  };
  keywords: string[];
  element?: string;
  astrology?: string;
  description: string;
  imageUrl: string;
}
```

### Spread Data Structure
```typescript
interface SpreadPosition {
  id: number;
  name: string;
  meaning: string;
  coordinates: {x: number, y: number};
  cardId?: number;
}

interface SpreadTemplate {
  id: string;
  name: string;
  description: string;
  positions: SpreadPosition[];
  timeEstimate: number;
  difficulty: 'beginner' | 'intermediate' | 'advanced';
}
```

### Reading Session Data
```typescript
interface ReadingSession {
  id: string;
  readerId: string;
  spreadType: string;
  cards: {
    position: number;
    cardId: number;
    isReversed: boolean;
    notes: string;
  }[];
  timestamp: Date;
  duration: number;
  notes: string;
  screenshots: string[];
}
``` 