
# 🚀 DevOps Web Page Deployment using Nginx on EC2

This project demonstrates how to deploy a **static DevOps-themed HTML web page** using the **Nginx web server** on a Linux-based EC2 instance. It covers installation, configuration, file deployment, and accessing the website via a public IP.

---

## 📘 What is Nginx?

**Nginx** (pronounced "engine-x") is a high-performance web server and reverse proxy. It efficiently serves static content, acts as a load balancer, and handles multiple client connections concurrently. It is widely used in DevOps pipelines for deployment and delivery of modern web applications.

---

## 🛠️ Steps to Deploy

### ⚙️ Step 1: Install and Verify Nginx

```bash
sudo apt-get update
sudo apt-get install nginx -y
sudo systemctl status nginx
```

Make sure the Nginx service is **active (running)**.

---

### 📁 Step 2: Navigate to Web Directory

```bash
cd /var
ls
```

You’ll find a directory named `www` where web content is stored.
![Screenshot 2025-06-15 153249](https://github.com/user-attachments/assets/51b0cc5a-8472-47f1-91bb-20ceb98453b6)


---

### 📁 Step 3: Explore the `www` Directory

```bash
cd www
ls
```

You’ll see the `html` directory, which is the default document root for Nginx.

---

### 📂 Step 4: Enter the `html` Directory

```bash
cd html
```

This is where you place your website files.

---
![Screenshot 2025-06-15 153355](https://github.com/user-attachments/assets/7824ec93-3047-4b4f-b2ff-60ecaf402396)

### ✍️ Step 5: Create Your Custom Web Page

```bash
sudo vim index.html
```

Paste your HTML content, for example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DevOps Junoon - Batch 9</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #6e48aa;
            --secondary: #9d50bb;
            --dark: #1a1a2e;
            --light: #f8f9fa;
            --accent: #41d3bd;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: var(--dark);
            color: var(--light);
            overflow-x: hidden;
            background-image: 
                radial-gradient(circle at 25% 25%, rgba(110, 72, 170, 0.15) 0%, transparent 50%),
                radial-gradient(circle at 75% 75%, rgba(157, 80, 187, 0.15) 0%, transparent 50%);
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }
        
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            margin-bottom: 3rem;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 1rem;
        }
        
        .logo i {
            font-size: 2.5rem;
            color: var(--accent);
        }
        
        .logo-text h1 {
            font-size: 1.8rem;
            background: linear-gradient(to right, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            font-weight: 700;
        }
        
        .logo-text p {
            font-size: 0.9rem;
            opacity: 0.8;
        }
        
        nav ul {
            display: flex;
            gap: 2rem;
            list-style: none;
        }
        
        nav a {
            color: var(--light);
            text-decoration: none;
            font-weight: 500;
            transition: all 0.3s ease;
            position: relative;
        }
        
        nav a:hover {
            color: var(--accent);
        }
        
        nav a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--accent);
            transition: width 0.3s ease;
        }
        
        nav a:hover::after {
            width: 100%;
        }
        
        .hero {
            text-align: center;
            padding: 5rem 0;
            position: relative;
        }
        
        .hero h2 {
            font-size: 3.5rem;
            margin-bottom: 1.5rem;
            background: linear-gradient(to right, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .hero p {
            font-size: 1.2rem;
            max-width: 700px;
            margin: 0 auto 2rem;
            opacity: 0.9;
            line-height: 1.6;
        }
        
        .cta-button {
            display: inline-block;
            padding: 0.8rem 2rem;
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            color: white;
            border-radius: 50px;
            text-decoration: none;
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(110, 72, 170, 0.4);
            border: none;
            cursor: pointer;
        }
        
        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(110, 72, 170, 0.6);
        }
        
        .tech-icons {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin-top: 3rem;
            flex-wrap: wrap;
        }
        
        .tech-icon {
            font-size: 3rem;
            color: var(--accent);
            transition: all 0.3s ease;
        }
        
        .tech-icon:hover {
            transform: translateY(-5px) scale(1.1);
        }
        
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin: 5rem 0;
        }
        
        .feature-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 2rem;
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
        }
        
        .feature-card:hover {
            transform: translateY(-10px);
            background: rgba(255, 255, 255, 0.1);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
        
        .feature-card i {
            font-size: 2.5rem;
            margin-bottom: 1.5rem;
            color: var(--accent);
        }
        
        .feature-card h3 {
            font-size: 1.5rem;
            margin-bottom: 1rem;
        }
        
        .feature-card p {
            opacity: 0.8;
            line-height: 1.6;
        }
        
        footer {
            text-align: center;
            padding: 2rem 0;
            margin-top: 5rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .social-links {
            display: flex;
            justify-content: center;
            gap: 1.5rem;
            margin: 1.5rem 0;
        }
        
        .social-links a {
            color: var(--light);
            font-size: 1.5rem;
            transition: all 0.3s ease;
        }
        
        .social-links a:hover {
            color: var(--accent);
            transform: translateY(-3px);
        }
        
        .particles {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            overflow: hidden;
        }
        
        .particle {
            position: absolute;
            background: rgba(255, 255, 255, 0.5);
            border-radius: 50%;
            animation: float linear infinite;
        }
        
        @keyframes float {
            0% {
                transform: translateY(0) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) rotate(360deg);
                opacity: 0;
            }
        }
        
        @media (max-width: 768px) {
            header {
                flex-direction: column;
                gap: 1.5rem;
            }
            
            nav ul {
                gap: 1rem;
            }
            
            .hero h2 {
                font-size: 2.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="particles" id="particles"></div>
    
    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-code-branch"></i>
                <div class="logo-text">
                    <h1>DevOps Junoon</h1>
                    <p>Batch 9 - Cloud Champions</p>
                </div>
            </div>
            <nav>
                <ul>
                    <li><a href="#"><i class="fas fa-home"></i> Home</a></li>
                    <li><a href="#"><i class="fas fa-users"></i> Batch</a></li>
                    <li><a href="#"><i class="fas fa-project-diagram"></i> Projects</a></li>
                    <li><a href="#"><i class="fas fa-graduation-cap"></i> Resources</a></li>
                    <li><a href="#"><i class="fas fa-envelope"></i> Contact</a></li>
                </ul>
            </nav>
        </header>
        
        <section class="hero">
            <h2>Welcome to DevOps Junoon Batch 9</h2>
            <p>Where passion meets infrastructure. Join us on this transformative journey from code to cloud, mastering the tools and practices that power modern software delivery.</p>
            <a href="#" class="cta-button">Join the Revolution</a>
            
            <div class="tech-icons">
                <i class="fab fa-docker tech-icon" title="Docker"></i>
                <i class="fab fa-kubernetes tech-icon" title="Kubernetes"></i>
                <i class="fab fa-aws tech-icon" title="AWS"></i>
                <i class="fab fa-jenkins tech-icon" title="Jenkins"></i>
                <i class="fab fa-git-alt tech-icon" title="Git"></i>
                <i class="fab fa-linux tech-icon" title="Linux"></i>
                <i class="fab fa-python tech-icon" title="Python"></i>
            </div>
        </section>
        
        <section class="features">
            <div class="feature-card">
                <i class="fas fa-rocket"></i>
                <h3>CI/CD Pipelines</h3>
                <p>Master continuous integration and deployment with industry-standard tools like Jenkins, GitHub Actions, and ArgoCD.</p>
            </div>
            
            <div class="feature-card">
                <i class="fas fa-cloud"></i>
                <h3>Cloud Native</h3>
                <p>Build and deploy scalable applications using Kubernetes, Docker, and cloud platforms like AWS and Azure.</p>
            </div>
            
            <div class="feature-card">
                <i class="fas fa-shield-alt"></i>
                <h3>DevSecOps</h3>
                <p>Integrate security into your workflow with tools like Trivy, Aqua Security, and OPA Gatekeeper.</p>
            </div>
            
            <div class="feature-card">
                <i class="fas fa-network-wired"></i>
                <h3>Infrastructure as Code</h3>
                <p>Automate your infrastructure provisioning with Terraform, Ansible, and Pulumi.</p>
            </div>
            
            <div class="feature-card">
                <i class="fas fa-chart-line"></i>
                <h3>Monitoring & Logging</h3>
                <p>Implement observability with Prometheus, Grafana, ELK stack, and OpenTelemetry.</p>
            </div>
            
            <div class="feature-card">
                <i class="fas fa-users-cog"></i>
                <h3>Collaborative Learning</h3>
                <p>Join a community of passionate learners with hands-on projects, code reviews, and pair programming.</p>
            </div>
        </section>
        
        <footer>
            <p>© 2023 DevOps Junoon - Batch 9 | Cloud Champions</p>
            <div class="social-links">
                <a href="#"><i class="fab fa-github"></i></a>
                <a href="#"><i class="fab fa-linkedin"></i></a>
                <a href="#"><i class="fab fa-twitter"></i></a>
                <a href="#"><i class="fab fa-youtube"></i></a>
                <a href="#"><i class="fab fa-discord"></i></a>
            </div>
            <p>Made with <i class="fas fa-heart" style="color: #e74c3c;"></i> by DevOps Junoon Team</p>
        </footer>
    </div>

    <script>
        // Create floating particles
        document.addEventListener('DOMContentLoaded', function() {
            const particlesContainer = document.getElementById('particles');
            const particleCount = 30;
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.classList.add('particle');
                
                // Random size between 2px and 6px
                const size = Math.random() * 4 + 2;
                particle.style.width = `${size}px`;
                particle.style.height = `${size}px`;
                
                // Random position
                particle.style.left = `${Math.random() * 100}%`;
                particle.style.top = `${Math.random() * 100}%`;
                
                // Random animation duration between 10s and 20s
                const duration = Math.random() * 10 + 10;
                particle.style.animationDuration = `${duration}s`;
                
                // Random delay
                particle.style.animationDelay = `${Math.random() * 5}s`;
                
                particlesContainer.appendChild(particle);
            }
        });
    </script>
</body>
</html>
```

To save and exit in `vim`:
- Press `Esc`
- Type `:wq`
- Hit `Enter`

---

### 🌐 Step 6: Access Your Website

Get your EC2 instance’s **public IP address**, then open it in a browser:

```
http://<your-public-ip>:80
```

📌 Example:

```
http://18.200.234.22:80
```

You should see your custom DevOps webpage live!

---

## ✅ Conclusion

You’ve successfully deployed a static web page using **Nginx** on an **EC2 instance**. This is a foundational step in DevOps and cloud-based web deployments.

---

