# Automating HTTP Server Setup with Ansible and AWS Systems Manager

This project contains an Ansible playbook designed to automate the setup of an HTTP server and deploy a dynamic website to your EC2 instances. It leverages AWS Systems Manager's **AWS-ApplyAnsiblePlaybooks** document to execute commands directly on managed instances.

---

## Features

- **Automated HTTP Server Installation**: Installs and configures Apache HTTP Server.
- **Dynamic Website Deployment**: Generates a unique website for each server using the current timestamp.
- **Firewall Configuration**: Configures the firewall to allow HTTP traffic.
- **AWS Systems Manager Integration**: Executes the playbook seamlessly on your managed EC2 instances.

---

## File Structure

```
project/
├── setup_http_server.yml         # The main Ansible playbook
├── README.md                     # Documentation for the project
```

---

## Prerequisites

1. **AWS Account**: Ensure you have an AWS account with appropriate permissions.
2. **Managed Instances**:
   - Configure your EC2 instances as **Managed Nodes** in AWS Systems Manager.
   - Attach an IAM role with the **AmazonSSMManagedInstanceCore** policy to your instances.
3. **Playbook Storage**:
   - Upload the playbook to an **S3 bucket** or a **GitHub repository** accessible by AWS Systems Manager.

---

## Usage

### 1. Upload the Playbook

- **S3**: Upload the playbook file (`setup_http_server.yml`) to an S3 bucket.
- **GitHub**: Commit the playbook to a public or private GitHub repository.

### 2. Run the Playbook via AWS Systems Manager

1. Open the AWS Management Console and navigate to **Systems Manager** > **Run Command**.
2. Select the document **AWS-ApplyAnsiblePlaybooks**.
3. Specify the playbook source:
   - **S3**: `s3://your-bucket-name/setup_http_server.yml`
   - **GitHub**: `https://github.com/your-repo/your-playbooks.git`
4. Choose target instances by ID, tags, or resource group.
5. Execute the command and monitor its status.

---

## Example Commands

### Run Playbook Locally (Optional)

To test the playbook locally before deploying via Systems Manager:

1. Create an inventory file (`inventory.ini`):
   ```ini
   [webservers]
   localhost ansible_connection=local
   ```
2. Run the playbook:
   ```bash
   ansible-playbook -i inventory.ini setup_http_server.yml
   ```

---

## Output

After successful execution:
- The HTTP server will be installed and running.
- The website will be accessible at `http://<server-public-ip>` and will display a unique timestamp.
