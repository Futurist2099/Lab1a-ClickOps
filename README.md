# Lab1a-ClickOps

Student Deliverables:
1) Screenshot of:
  RDS SG inbound rule using source - done
  EC2 role attached - done
  /list output showing at least 3 notes - done
  
  
2) Short answers:
  A) Why is DB inbound source restricted to the EC2 security group?    
       Answer = To keep RDS access only on the private subnets via the EC2 as a public bastion
  
  B) What port does MySQL use?
      Answer = 3306
	  
  C) Why is Secrets Manager better than storing creds in code/user-data?
      Answer = Auto-rotate pwd token daily / in case the EC2 gets hacked, the creds are not hard-coded
  
  
3) Evidence for Audits / Labs (Recommended Output)

      aws ec2 describe-security-groups --group-ids sg-0123456789abcdef0 > sg.json
      aws rds describe-db-instances --db-instance-identifier mydb01 > rds.json
      aws secretsmanager describe-secret --secret-id my-db-secret > secret.json
      aws ec2 describe-instances --instance-ids i-0123456789abcdef0 > instance.json
      aws iam list-attached-role-policies --role-name MyEC2Role > role-policies.json
	  
	  
4) 
Then Answer:

Why each rule exists & why broader access is forbidden
	a & b) Designed to limit public access via network design so that the chances of data breaches are minimized

What would break if removed
	c) The link between the EC2 and Database
	
Why this role exists
	d) To avoid hard-coding the admin pwd
	
Why it can read this secret
	e) Using the auto-rotating token
	
Why it cannot read others
	f) Not setup via IAM access
