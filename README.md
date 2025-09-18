# 📊 Ansible VM Monitoring & Email Reporting

This project automates the monitoring of AWS EC2 instances (VMs) using Ansible. It collects system metrics (CPU, memory, disk usage) from multiple VMs and sends a consolidated HTML report via email.

## 🚀 Features

- Collects VM metrics:
  - ✅ CPU usage
  - ✅ Memory usage
  - ✅ Disk usage
- Works across Debian/Ubuntu and RedHat/CentOS
- Consolidates results from all VMs
- Sends a beautiful HTML email report with metrics
- Uses Ansible Master → Slave architecture

## 🛠️ Technologies Used

- **AWS EC2** – Virtual machines for testing & deployment
- **Ansible** – Automation engine
- **YAML** – Playbook configuration
- **Sysstat** – For system statistics (mpstat)
- **Linux Shell Commands** – For collecting metrics
- **SMTP** – For sending email reports

## 📂 Project Structure

```
ansible-vm-monitoring/
│── group_vars/                  
│   └── all.yml                  # Global variables (SMTP/email settings)
│── inventory/                   
│   └── aws_ec2_ip.yml           # AWS EC2 inventory file with target VM IPs
│── templates/
│   └── report_email.html.j2     # Jinja2 template for HTML email report
│── collect_metrics.yml          # Playbook: Collects CPU, memory, disk usage
│── send_report.yml              # Playbook: Sends consolidated HTML report
│── playbook.yml                 # Master playbook (can include others)
│── ansible.cfg                  # Ansible configuration
│── README.md                    # Project documentation

```

## ⚙️ How It Works

### 1️⃣ Collect Metrics (collect_metrics.yml)
- Installs sysstat (mpstat) depending on OS
- Collects:
  - CPU usage using mpstat
  - Memory usage using free
  - Disk usage using df
- Stores metrics in Ansible facts (vm_metrics)

### 2️⃣ Send Report (send_report.yml)
- Gathers all VM metrics into one consolidated list
- Formats data into HTML email (Jinja2 template)
- Sends report via SMTP

## ▶️ Usage

### 1. Clone the repo
```bash
git clone https://github.com/your-username/ansible-vm-monitoring.git
cd ansible-vm-monitoring
```

### 2. Update inventory file
Add your Ansible master and slave nodes in `inventory/hosts`.

Example:
```ini
[master]
ansible-master ansible_host=192.168.1.10

[slaves]
web-server-1 ansible_host=192.168.1.11
web-server-2 ansible_host=192.168.1.12
db-server-1 ansible_host=192.168.1.13

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/aws_key.pem
```

### 3. Configure SMTP settings
Edit `group_vars/all.yml`:

```yaml
# SMTP Configuration
smtp_server: "smtp.gmail.com"
smtp_port: 587
email_user: "your_email@gmail.com"
email_pass: "your_password_or_app_key"
alert_recipient: "recipient_email@gmail.com"

# Report Configuration
report_subject: "Daily VM Metrics Report"
company_name: "Your Company Name"
```

### 4. Run playbooks
Collect VM metrics:
```bash
ansible-playbook -i inventory/hosts playbooks/collect_metrics.yml
```

Send email report:
```bash
ansible-playbook -i inventory/hosts playbooks/send_report.yml
```

## 📜 License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgements

- [Ansible Documentation](https://docs.ansible.com/)
- [AWS Free Tier](https://aws.amazon.com/free/) for testing environment
- [Sysstat](https://github.com/sysstat/sysstat) for system performance monitoring

---
