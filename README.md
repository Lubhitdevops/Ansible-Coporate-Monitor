📊 Ansible VM Monitoring & Email Reporting

This project automates the monitoring of AWS EC2 instances (VMs) using Ansible.
It collects system metrics (CPU, memory, disk usage) from multiple VMs and sends a consolidated HTML report via email.

🚀 Features

Collects VM metrics:

✅ CPU usage

✅ Memory usage

✅ Disk usage

Works across Debian/Ubuntu and RedHat/CentOS

Consolidates results from all VMs

Sends a beautiful HTML email report with metrics

Uses Ansible Master → Slave architecture

🛠️ Technologies Used

AWS EC2 – Virtual machines for testing & deployment

Ansible – Automation engine

YAML – Playbook configuration

Sysstat – For system statistics (mpstat)

Linux Shell Commands – For collecting metrics

SMTP – For sending email reports

📂 Project Structure
ansible-vm-monitoring/
│── inventory/                  # Ansible inventory file (hosts: master, slaves)
│── playbooks/
│   ├── collect_metrics.yml     # Collects CPU, memory, disk metrics from VMs
│   ├── send_report.yml         # Sends consolidated HTML report via email
│── templates/
│   └── report_email_animated.html.j2   # Jinja2 HTML email template
│── group_vars/
│   └── all.yml                 # SMTP/email credentials and global vars
│── README.md                   # Project documentation
│── LICENSE                     # License file

⚙️ How It Works
1️⃣ Collect Metrics (collect_metrics.yml)

Installs sysstat (mpstat) depending on OS

Collects:

CPU usage using mpstat

Memory usage using free

Disk usage using df

Stores metrics in Ansible facts (vm_metrics)

2️⃣ Send Report (send_report.yml)

Gathers all VM metrics into one consolidated list

Formats data into HTML email (Jinja2 template)

Sends report via SMTP

▶️ Usage
1. Clone the repo
git clone https://github.com/your-username/ansible-vm-monitoring.git
cd ansible-vm-monitoring

2. Update inventory file

Add your Ansible master and slave nodes in inventory/hosts.

3. Configure SMTP settings

Edit group_vars/all.yml:

smtp_server: "smtp.gmail.com"
smtp_port: 587
email_user: "your_email@gmail.com"
email_pass: "your_password_or_app_key"
alert_recipient: "recipient_email@gmail.com"

4. Run playbooks
Collect VM metrics
ansible-playbook -i inventory/hosts playbooks/collect_metrics.yml

Send email report
ansible-playbook -i inventory/hosts playbooks/send_report.yml

📜 License

This project is licensed under the MIT License – see the LICENSE
 file for details.

🙏 Acknowledgements

Ansible Documentation

AWS Free Tier
 for testing environment

Sysstat
 for system performance monitoring
