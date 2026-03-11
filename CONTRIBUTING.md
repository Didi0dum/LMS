# Contributing to LMS (Light My Satellite)

**Thank you for your interest in contributing to LMS!** 🛰️

Whether you're a hardware enthusiast, software developer, astronomer, or student learning about space situational awareness — **your contributions are welcome here**.

This project has an ambitious vision: **a global network of 1,000+ satellite tracking stations**. Every contribution, no matter how small, brings us closer to that goal.

---

## 🌍 Our Vision

LMS aims to democratize space debris monitoring by making satellite tracking technology:
- **Accessible** — affordable hardware, whenever possible
- **Distributed** — deployed at universities, observatories, and amateur clubs worldwide
- **Open** — fully open-source for learning, modification, and improvement

**Your contribution helps build a safer orbital environment.**

---

## 🚀 Ways to Contribute

### 1. 🔧 Hardware Contributions
- **Alternative sensor configurations** — test different LiDAR models, camera systems, or hybrid approaches
- **Mechanical improvements** — weatherproofing, mounting solutions, cable management
- **Power optimization** — battery systems, solar integration, power consumption analysis
- **Documentation** — assembly guides, wiring diagrams, 3D printable parts

### 2. 💻 Software Contributions
- **Algorithm improvements** — Kalman filtering, predictive tracking, noise reduction
- **Performance optimization** — reduce latency, improve tracking accuracy
- **New features** — weather integration, TLE comparison, automated calibration
- **Bug fixes** — anything that doesn't work as expected
- **Testing** — write tests, improve test coverage, validate edge cases

### 3. 📊 Data & Science
- **Orbital mechanics** — improve trajectory prediction algorithms
- **TLE integration** — compare live observations with catalog data
- **Anomaly detection** — develop ML models for unusual orbital behavior
- **Calibration methods** — improve sensor fusion and coordinate transformation

### 4. 📚 Documentation & Education
- **User guides** — setup tutorials, troubleshooting guides
- **API documentation** — improve code comments and API references
- **Educational content** — lesson plans, workshop materials, demonstration videos
- **Translations** — documentation in other languages

### 5. 🎨 Visualization & UI
- **Frontend improvements** — better 3D visualization, mobile responsiveness
- **Dashboard enhancements** — real-time metrics, historical playback
- **Data export tools** — CSV, JSON, or custom formats
- **Mobile app development** — remote station monitoring

---

## 🛠️ Getting Started

### Development Environment Setup

#### Hardware Development
```bash
# Clone the repository with all submodules
git clone --recursive https://github.com/Didi0dum/LMS.git
cd LMS/lms-hardware

# Install Python dependencies
pip install -r requirements.txt

# See hardware/README.md for physical setup
```

#### Controller Development
```bash
cd LMS/lms-controller

# Install Bun (if not already installed)
curl -fsSL https://bun.sh/install | bash

# Install dependencies
bun install

# Start development environment
docker compose up -d  # Start MQTT + InfluxDB
bun run dev           # Start Elysia backend
cd frontend && bun run dev  # Start Next.js frontend
```

### Development Workflow

1. **Fork the repository** — Click "Fork" on GitHub
2. **Clone your fork** — `git clone https://github.com/YOUR_USERNAME/LMS.git`
3. **Create a branch** — `git checkout -b feature/your-feature-name`
4. **Make changes** — Write code, update docs, fix bugs
5. **Test thoroughly** — Ensure nothing breaks
6. **Commit with clear messages** — `git commit -m "Add: Kalman filter for position smoothing"`
7. **Push to your fork** — `git push origin feature/your-feature-name`
8. **Open a Pull Request** — Describe what you changed and why

---

## 📋 Code Style Guidelines

### Python (lms-hardware)

Follow **PEP 8** with these specifics:
```python
# Good
def track_elevation(
    station: LMSStation,
    lidar_lock: threading.Lock,
    stop_event: threading.Event,
    el_step: float = 3.0,
) -> None:
    """
    Track target elevation using dual LIDAR sensors.
    
    Args:
        station: LMS station instance
        lidar_lock: Thread lock for sensor access
        stop_event: Signal to stop tracking
        el_step: Angular step size in degrees
    """
    pass

# Bad
def track_elevation(station,lidar_lock,stop_event,el_step=3.0):
    pass  # No type hints, no docstring
```

**Key points:**
- Type hints for all function arguments and returns
- Docstrings for public functions (Google style)
- Maximum line length: 88 characters (Black formatter)
- Use `ruff` for linting: `ruff check .`

### TypeScript (lms-controller)

Follow **TypeScript strict mode** conventions:
```typescript
// Good
interface StationConfig {
  id: string;
  organizationId: string;
  location: {
    latitude: number;
    longitude: number;
    altitude: number;
  };
}

async function createStation(config: StationConfig): Promise<Station> {
  // Implementation
}

// Bad
function createStation(config: any) {
  // No types, no async/await clarity
}
```

**Key points:**
- Strict TypeScript mode enabled
- Explicit types (avoid `any`)
- Async/await over promise chains
- Use Biome for formatting: `bun run format`

---

## ✅ Testing Requirements

### Hardware Tests
```bash
# Run hardware component tests
cd lms-hardware
python -m pytest tests/

# Test individual components
python -m tests.drivers.lidar_test
python -m tests.drivers.stepper_test
```

### Controller Tests
```bash
# Run backend tests
cd lms-controller
bun test

# Run frontend tests
cd frontend
bun test
```

**Before submitting a PR:**
- [ ] All existing tests pass
- [ ] New features include tests
- [ ] Manual testing completed (if applicable)

---

## 🐛 Reporting Issues

### Bug Reports

Use this template when reporting bugs:
```markdown
**Description:**
Clear description of the bug

**To Reproduce:**
1. Step 1
2. Step 2
3. See error

**Expected Behavior:**
What should happen

**Actual Behavior:**
What actually happens

**Environment:**
- Hardware: Raspberry Pi 4B / 2GB
- OS: Raspberry Pi OS Bullseye
- Python: 3.11.2
- Component: lms-hardware / lms-controller

**Logs/Screenshots:**
Attach relevant logs or screenshots
```

### Feature Requests

Use this template for feature requests:
```markdown
**Feature Description:**
What feature would you like to see?

**Use Case:**
Why is this feature needed? Who benefits?

**Proposed Implementation:**
(Optional) How might this be implemented?

**Alternatives Considered:**
(Optional) Other approaches you've thought about
```

---

## 🔀 Pull Request Process

### Before Submitting

- [ ] Code follows style guidelines
- [ ] Tests pass locally
- [ ] Documentation updated (if applicable)
- [ ] Commit messages are clear
- [ ] Branch is up to date with `main`

### PR Description Template
```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Performance improvement
- [ ] Code refactoring

## Testing
How was this tested?

## Checklist
- [ ] Code follows project style
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] No breaking changes (or documented)

## Screenshots (if applicable)
Add screenshots for UI changes
```

### Review Process

1. **Automated checks** — CI/CD runs tests and linting
2. **Code review** — Maintainer reviews code quality
3. **Testing** — Changes tested on real hardware (if applicable)
4. **Merge** — PR merged into `main` branch
5. **Acknowledgment** — Contributors added to project credits

---

## 🤝 Code of Conduct

### Our Standards

**We are committed to providing a welcoming and inclusive environment.**

✅ **Do:**
- Be respectful and constructive
- Welcome newcomers and help them learn
- Give and accept constructive feedback gracefully
- Focus on what's best for the project and community

❌ **Don't:**
- Use offensive, discriminatory, or harassing language
- Make personal attacks or insults
- Share others' private information without permission
- Behave unprofessionally in project spaces

### Enforcement

Violations may result in:
1. Warning from maintainers
2. Temporary ban from project spaces
3. Permanent ban for repeated or severe violations

Report issues to: dilyana.k.vasileva@gmail.com

---

## 🎓 Learning Resources

### New to Satellite Tracking?
- [Satellite Laser Ranging Basics](https://ilrs.gsfc.nasa.gov/about/index.html)
- [TLE Format Explanation](https://en.wikipedia.org/wiki/Two-line_element_set)
- [Orbital Mechanics Primer](https://www.youtube.com/watch?v=fZq8LMO5ndA)

### New to Raspberry Pi?
- [Official Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/)
- [Python GPIO Guide](https://gpiozero.readthedocs.io/)
- [I2C Communication Tutorial](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c)

### New to Time-Series Databases?
- [InfluxDB Documentation](https://docs.influxdata.com/influxdb/)
- [MQTT Protocol Overview](https://mqtt.org/getting-started/)
- [Real-time Data Visualization](https://threejs.org/docs/)

---

## 💬 Communication

### Ask Questions
- **GitHub Discussions** — Best for general questions and ideas
- **GitHub Issues** — For bugs and feature requests
- **Email** — dilyana.k.vasileva@gmail.com / kiril.l.rangelov.2022@elsys-bg.org

### Stay Updated
- **Watch the repository** — Get notifications for new issues and PRs
- **Star the project** — Show your support and track progress

---

## 🏆 Recognition

Contributors are recognized in:
- **README.md** — Major contributors listed
- **Release notes** — Contributions acknowledged in each release
- **Git history** — Your commits are permanent project history

### Hall of Fame

We especially recognize contributions that:
- Enable new capabilities (e.g., first laser ranging integration)
- Significantly improve performance (e.g., 10x faster tracking)
- Expand accessibility (e.g., translations, educational content)
- Deploy the first international station (outside Bulgaria)

---

## 📊 Priority Areas (Help Wanted!)

### High Priority
1. **Kalman Filter Implementation** — Reduce coordinate noise
2. **Weather Station Integration** — Correlate tracking with atmospheric conditions
3. **TLE Catalog Integration** — Compare observations with predicted orbits
4. **Mobile App** — iOS/Android station monitoring

### Medium Priority
1. **Docker One-Command Deploy** — Simplify controller setup
2. **Automated Testing** — Increase test coverage to >80%
3. **Performance Benchmarks** — Standardized latency/accuracy metrics
4. **Simulation Environment** — Test algorithms without hardware

### Future Vision
1. **Laser Emitter Integration** — Transition to active ranging
2. **Multi-Station Coordination** — Handoff between stations
3. **Anomaly Detection ML** — Automatic orbit deviation alerts
4. **Public Dashboard** — Global map of active stations

---

## 🌟 First Contribution?

**Welcome!** Here are great places to start:

### Good First Issues
- Documentation improvements (fix typos, add examples)
- Code comments and docstrings
- Unit tests for existing functions
- Configuration file templates
- Setup troubleshooting guides

**Look for issues labeled:** `good-first-issue`, `documentation`, `help-wanted`

### Beginner-Friendly Tasks
1. Add type hints to Python functions missing them
2. Write tests for untested modules
3. Improve error messages for common failures
4. Add validation for configuration files
5. Create example configuration templates

**Don't hesitate to ask questions!** Every expert was once a beginner.

---

## 📜 License

By contributing to LMS, you agree that your contributions will be licensed under the **GNU License**.

This means:
- Your code can be used freely
- You retain copyright to your contributions
- You grant others the right to use your code under GNU terms

---

## 🙏 Thank You!

**Every contribution matters.** Whether you:
- Fix a typo in documentation
- Report a bug you encountered
- Add a major new feature
- Deploy the 100th station in the network

**You're helping build a safer orbital environment.**

Together, we're proving that world-class space technology doesn't require world-class budgets — just curiosity, collaboration, and commitment to the mission.

**Welcome to the LMS community!** 🛰️

---

<div align="center">

*"The best time to plant a tree was 20 years ago. The second best time is now."*

**Let's build the future of distributed space monitoring — together.**

[![Contributors](https://img.shields.io/github/contributors/Didi0dum/LMS?style=for-the-badge)](https://github.com/Didi0dum/LMS/graphs/contributors)

</div>