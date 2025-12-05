# 🚀 Panduan Deploy SOSYA Landing Page ke Coolify

## Prerequisites
- Akun Coolify (https://coolify.io)
- Git repository sudah ter-setup
- Domain yang sudah siap (opsional, bisa pakai IP dulu)

---

## 📋 Langkah-Langkah Deploy

### 1. Setup di Coolify Dashboard
```
1. Login ke dashboard Coolify: https://coolify.sosya.app
2. Pilih "Projects" → "New Project"
3. Beri nama: "SOSYA Landing Page"
4. Klik "Create"
```

### 2. Tambah Service
```
1. Di project, klik "+ New" → "Public Repository"
2. Pilih "Docker" sebagai service type
3. Konfigurasi:
   - Repository URL: https://github.com/sosyaapp/sosyaapp-landingpage
   - Branch: main
   - Build method: Dockerfile
   - Base Directory: ./ (atau kosongkan untuk root)
```

### 3. Environment Variables (jika diperlukan)
```
Di tab "Environment Variables", tambahkan:
- NODE_ENV=production
```

### 4. Port Configuration
```
- Ports Exposes: 80
```

### 5. Domain Setup
```
1. Klik tab "Domains"
2. Tambah domain baru atau gunakan subdomain Coolify
3. Atur DNS pointing ke IP Coolify Anda
4. Generate SSL Certificate (auto dengan Let's Encrypt)
```

### 6. Deploy
```
1. Review semua konfigurasi
2. Klik "Deploy" / "Save & Deploy"
3. Tunggu build process (biasanya 2-5 menit)
4. Check logs di tab "Logs"
```

---

## 🔧 Konfigurasi File yang Sudah Dibuat

### 1. **Dockerfile**
- Multi-stage build untuk optimization
- Nginx sebagai web server
- Health check included
- Gzip compression enabled

### 2. **nginx.conf**
- SPA routing fallback ke index.html
- Gzip compression untuk assets
- Cache control headers
- Security headers (X-Frame-Options, CSP, dll)
- WebP image support

### 3. **docker-compose.yml**
- Local development dengan Docker
- Network isolated
- Auto-restart policy
- Health checks

### 4. **.dockerignore**
- Exclude file yang tidak perlu di image
- Reduce final image size

---

## 🔍 Cek Status Deploy

### Di Coolify Dashboard:
1. **Logs Tab** - Lihat real-time logs
2. **Stats Tab** - Monitor CPU, Memory usage
3. **Health Check** - Green = OK, Red = Error

### Via Terminal:
```bash
# SSH ke Coolify server
ssh root@your-coolify-ip

# Check container
docker ps | grep sosya-landing

# View logs
docker logs sosya-landing -f

# Test endpoint
curl http://localhost/
```

---

## 📊 Performance Optimization

✅ **Sudah dioptimasi di project:**
- Webp images untuk faster loading
- Gzip compression di nginx
- Cache control headers
- Minified CSS/JS (via Tailwind CDN)
- Security headers

### Monitoring di Coolify:
- CPU usage
- Memory usage
- Network I/O
- Response times
- Error rates

---

## 🚨 Troubleshooting

### Build Failed
```
→ Check Dockerfile syntax
→ Verify nginx.conf is valid
→ Check docker-compose.yml format
```

### Port Already in Use
```
→ Change published port di Coolify
→ Atau shutdown service lain di port 80
```

### Domain Not Resolving
```
→ Check DNS A record pointing ke Coolify IP
→ Wait max 48 hours untuk DNS propagation
→ Verify SSL certificate generated
```

### Images Not Loading
```
→ Check assets/images/ folder path
→ Verify .webp file format
→ Check nginx.conf webp MIME type
```

---

## 📱 Testing Endpoints

```
Homepage:     http://your-domain.com/
Tentang:      http://your-domain.com/tentang.html
Bantuan:      http://your-domain.com/bantuan.html
Sitemap:      http://your-domain.com/sitemap.xml
Robots:       http://your-domain.com/robots.txt
```

---

## 🔐 Security Checklist

- ✅ SSL Certificate (Let's Encrypt)
- ✅ Security headers di nginx
- ✅ DDoS protection (enable di Coolify)
- ✅ Hide Nginx version (nginx.conf)
- ✅ robots.txt & sitemap.xml configured

---

## 🎯 Next Steps

1. **Monitor Performance**
   - Google Search Console integration
   - Analytics tracking
   - Error monitoring

2. **Optimize SEO**
   - Submit sitemap ke GSC
   - Monitor keyword rankings
   - Check Core Web Vitals

3. **Scale (if needed)**
   - Enable caching layer (Cloudflare)
   - CDN untuk images
   - Database untuk dynamic content

---

## 📞 Support

- Coolify Docs: https://docs.coolify.io
- GitHub Issues: https://github.com/sosyaapp/sosyaapp-landingpage/issues
- Community: https://community.coolify.io

Happy deploying! 🎉
