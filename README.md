# AWS Testnet Validator Templates

A collection of AWS Cloudformation templates for provisioning a self-updating validator. No frills here, I haven't included any swarm_key backup, monitoring, CloudWatch agents, AWS CLI installation, etc etc. 

## Installation

1. Clone the repo
2. Go to AWS
3. Create an SSH key pair within the EC2 dashboard. This will need to be done per AWS Region you intend to deploy your testnet validator. For example, if you want deploy validators in US-East-1 and US-East-2, you'll need to repeat step (3) in both Regions. After you've downloaded your key, you'll need to run the following on your local device to configure the necessary permissions:
```bash
chmod 400 <your-key-pair.pem>
```
4. Take note of the AMI ID for the Ubuntu 20.04-amd64 Image. I will update this with other Regions when I have time, but for reference:
- US-East-1: ami-042e8287309f5df03
- US-East-2: ami-08962a4068733a2b6 
- AP-East-1: ami-0d758c1134823146a
5. Go to the Cloudformation dashboard
6. First deploy the "testnet-validator-sg-template.yaml" file to create a Region-specific Security Group for your EC2 instances. Similar to point (3), this will need to per Region. 
7. Next deploy the "testnet-validator-ec2-template.yaml" file to create an EC2 running the Docker validator image. You can repeat step (7) as many times as you'd like to create as many instances as you'd like.
8. Voila, your validator will be deployed and will check whether updating is needed every hour, and will self-update if so. No checks for whether or not the validator is in CG.

I should note that I've set an alias so that you can access your validator as follows:
```bash
vld <validator commands>
```
e.g.,
```bash
vld info height
```
## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)