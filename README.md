# 🎬 Stremio Addon Manager

[![Vue.js](https://img.shields.io/badge/Vue.js-3.x-4FC08D?style=for-the-badge&logo=vue.js&logoColor=white)](https://vuejs.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](http://makeapullrequest.com)

> **A powerful web-based tool to manage and reorder your Stremio addons with ease**

## ✨ Features

- 🔄 **Drag & Drop Reordering** - Easily reorder your addons using an intuitive drag-and-drop interface
- 🛡️ **Safe & Secure** - Direct integration with Stremio's official API (api.strem.io)
- 💾 **Backup & Restore** - Export and import your addon configurations
- 🎯 **Smart Management** - Remove non-protected addons and configure existing ones
- 📱 **Responsive Design** - Works perfectly on desktop, tablet, and mobile devices
- 🌙 **Dark Mode Support** - Beautiful dark and light themes
- 🔐 **Privacy First** - No backend server, everything runs in your browser

## 🚀 Quick Start

### Prerequisites
- A Stremio account
- Modern web browser (Chrome, Firefox, Safari, Edge)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/stremio-addon-manager.git
   cd stremio-addon-manager
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start development server**
   ```bash
   npm run dev
   ```

4. **Open your browser**
   Navigate to `http://localhost:5173`

## 🏗️ Development

### Recommended IDE Setup

- [VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (disable Vetur)
- [Vue DevTools](https://devtools.vuejs.org/) for debugging

### Available Scripts

```bash
# Development with hot-reload
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Lint and fix files
npm run lint
```

## 🐳 Docker Deployment

### Quick Docker Setup

```bash
# Build the Docker image
docker build -t stremio-addon-manager .

# Run the container
docker run -p 8080:80 stremio-addon-manager
```

The application will be available at `http://localhost:8080`

### Docker Compose (Optional)

```yaml
version: '3.8'
services:
  stremio-addon-manager:
    build: .
    ports:
      - "8080:80"
    restart: unless-stopped
```

## 🔧 How It Works

### Authentication
1. **Login to Stremio Web** - Visit [web.stremio.com](https://web.stremio.com/)
2. **Get Auth Key** - Open browser console and run: `JSON.parse(localStorage.getItem("profile")).auth.key`
3. **Paste Key** - Enter the auth key in the application

### Managing Addons
1. **Load Addons** - Your addons will load automatically after authentication
2. **Reorder** - Drag and drop addons to your preferred order
3. **Sync** - Click "Sync to Stremio" to apply changes
4. **Backup** - Export your configuration for safekeeping

## 🛡️ Security & Privacy

- **Direct API Access** - All requests go directly to Stremio's official API
- **No Data Storage** - Credentials are never stored, only kept in memory
- **Client-Side Only** - No backend server, everything runs in your browser
- **Open Source** - Full transparency, review the code yourself

## ⚠️ Important Notice

> **This tool has been tested and is safe to use, but we recommend backing up your addon list before making any changes. We are not liable if anything breaks on your account.**

This is **not** an official Stremio product. Use at your own risk.

## 🤝 Contributing

We welcome contributions! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

Special thanks to our contributors:

- [**TVDOfficial**](https://github.com/TVDOfficial) - For contributions and support
- [**sleeyax**](https://github.com/sleeyax) - For conversations and code snippets that made this implementation possible

Big thank you to `Sleeyax` and `<Code/>` for the conversations and code snippets that made this really easy to implement.

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/your-username/stremio-addon-manager/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-username/stremio-addon-manager/discussions)

---

<div align="center">
  <p>Made with ❤️ for the Stremio community</p>
  <p>
    <a href="https://stremio.com">Stremio</a> •
    <a href="https://vuejs.org">Vue.js</a> •
    <a href="https://vitejs.dev">Vite</a>
  </p>
</div>
