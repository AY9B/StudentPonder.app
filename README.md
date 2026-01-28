# StudentPonder.app
# Student Ponder - iOS App

A comprehensive mental health and wellbeing platform for students.

## Features

### 🔐 Authentication
- Gmail login integration
- Microsoft account login
- Secure user session management

### 💬 Student Forum
- Share experiences with fellow students
- Post updates and thoughts
- View community discussions
- Reply to posts

### 🔍 Mental Health Resources
- Searchable database of mental health topics
- Topics include: Anxiety, Depression, Stress Management, Sleep Issues, Social Anxiety, Time Management, Eating Disorders, Loneliness
- Keyword-based search functionality
- Crisis hotline information

### 📔 Daily Diary
- Private journaling space
- Date-stamped entries
- Persistent storage (entries saved between sessions)
- View past entries
- Express thoughts and feelings freely

### 📊 Weekly Mood Tracker
- Track daily mood (Happy, Neutral, Sad)
- 7-day weekly tracking
- Automatic mood average calculation
- Visual mood indicators
- Reset functionality for new weeks

### ℹ️ About Page
- App mission and information
- Feature descriptions
- Privacy and security information
- Crisis resources

## Technical Stack

- **Framework**: React with Hooks
- **Icons**: Lucide React
- **Styling**: Tailwind CSS (utility classes)
- **Storage**: Persistent browser storage API
- **Fonts**: Playfair Display (headers), Poppins (body)

## Data Persistence

The app uses the browser's persistent storage API to save:
- Diary entries
- Weekly mood data
- User authentication state

All data persists between sessions and app restarts.

## Integrating with Xcode

### Option 1: WebView Wrapper (Easiest)

1. **Create a new iOS project in Xcode:**
   - Open Xcode
   - Create new project → iOS → App
   - Name it "Student Ponder"
   - Choose Swift and SwiftUI

2. **Add WKWebView to load the React app:**

```swift
import SwiftUI
import WebKit

struct ContentView: View {
    var body: some View {
        WebView()
            .edgesIgnoringSafeArea(.all)
    }
}

struct WebView: UIViewRepresentable {
    func makeUIView(context: Context) -> WKWebView {
        let webView = WKWebView()
        
        // Enable storage
        let config = webView.configuration
        config.websiteDataStore = .default()
        
        // Load your hosted React app
        if let url = URL(string: "YOUR_HOSTED_APP_URL") {
            let request = URLRequest(url: url)
            webView.load(request)
        }
        
        return webView
    }
    
    func updateUIView(_ webView: WKWebView, context: Context) {}
}
```

3. **Host the React app:**
   - Deploy `student-ponder.jsx` to a hosting service (Vercel, Netlify, etc.)
   - Update `YOUR_HOSTED_APP_URL` with your deployed URL

### Option 2: Native iOS App (Advanced)

Convert the React components to native SwiftUI:

1. **Create Models:**
```swift
struct DiaryEntry: Identifiable, Codable {
    let id: Int
    let content: String
    let date: String
    let timestamp: String
}

struct ForumPost: Identifiable, Codable {
    let id: Int
    let author: String
    let content: String
    let replies: Int
    let timestamp: String
}

struct User: Codable {
    let name: String
    let email: String
    let provider: String
}
```

2. **Create ViewModels and Views** for each page
3. **Use UserDefaults or CoreData** for persistence
4. **Implement OAuth** for Gmail and Microsoft login

### Option 3: React Native (Alternative)

Convert to React Native for true cross-platform mobile experience:

1. Initialize React Native project
2. Convert web components to React Native components
3. Use AsyncStorage for data persistence
4. Implement native OAuth libraries

## Deployment Options

### Web Deployment
- Deploy to Vercel, Netlify, or GitHub Pages
- Access via mobile browser or WebView wrapper

### Progressive Web App (PWA)
- Add service worker for offline functionality
- Enable "Add to Home Screen" on iOS
- Acts like a native app

### Full Native App
- Build in Swift/SwiftUI for iOS
- Submit to App Store

## Required Packages for React

```json
{
  "dependencies": {
    "react": "^18.0.0",
    "react-dom": "^18.0.0",
    "lucide-react": "^0.263.1"
  }
}
```

## Styling Requirements

Include these fonts in your HTML:
```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
```

## Security Considerations

1. **Authentication**: Currently uses simplified OAuth flow - implement proper OAuth 2.0 for production
2. **Data Storage**: Browser storage is used - consider encrypted storage for sensitive data
3. **HTTPS**: Always use HTTPS in production
4. **API Keys**: Store securely, never expose in client code

## Future Enhancements

- Push notifications for forum replies
- Professional counselor matching
- Group therapy sessions
- Integration with university counseling services
- Data export functionality
- Dark mode support
- Multi-language support
- Accessibility improvements

## Privacy & Ethics

- All diary entries are private and stored locally
- Forum posts are community-visible
- No data is shared without user consent
- Crisis resources prominently displayed
- Not a replacement for professional mental health care

## Support Resources

The app includes these crisis resources:
- **US**: National Suicide Prevention Lifeline - 988
- **UK**: Samaritans - 116 123
- **Crisis Text Line**: Text HOME to 741741

## License

This app is designed for educational purposes and student wellbeing support.

## Contact

For questions or support, contact your institution's IT or counseling services.

---

**Important Note**: This app provides peer support and self-help tools but is NOT a substitute for professional mental health care. Users experiencing crisis situations should contact emergency services or crisis hotlines immediately.
