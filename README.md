# HyperledgerFabric

Note: This documentation presents the codes and the intructions on how to use fabric samples application which are based onto the intructions given to us during our training in Hyperledger. All source codes are from MR. Johnny Zarate.

The fabric-samples application provides all the mandatory and optional function needed in the Project of Invoice (assignment.pptx)

Environment: 

Host: 
Operating System:Windows 8 (64-bit) 
Processor:Intel Core i3 
Storage: 4GB RAM / 500gb HHD
Virtualization software: VMware Workstation Pro 15 (VirtualBox 5.2.22 will do)
Guest: Ubuntu 16.04.5 LTS (64-bit), Config: 4GB RAM / 40GB Storage


Table of Contents

A. Materials

B. Set-up instructions

C. How to use

D. Troubleshooting



A. Prerequisites:

1. Make sure that Go (golang) is properly installed, as well as Postman is installed in your machine (SEE HyperledgerPrerequisite file for installation guide.).

2. Clone the fabric-repository from (https://github.com/khrandm/blockchain-training-labs) make sure that the fabric-samples is finished or working properly.

B. Set-up instructions:

1. Replace files (or backup before replacing) on your fabric-samples/chaincode/fabcar/go and fabric-samples/fabcar directories with the ones inside this repository (do not copy the node_module folder).

3. From the fabric-samples folder go to fabcar and right click and open terminal.

4. Enter './openScm.sh' (command to start Scm.sh)

5. Enter 'npm install' (command to install node module) 

5. Enter 'node enrollAdmin.sh' (command to create your admin).

6. Enter 'node registerUser.sh' (command to register new or another user OPTIONAL)

7. Enter node 'rSupplier1.sh' (command to register new or another supplier OPTIONAL)

8. Enter 'node rOEM.sh' (command to register OEM(original equipment manufacturer) user )

9. To test all functions, Enter node app_scm.sh

10. To test as supplier1, open a new Terminal window, type and press Enter: node appSupplier1.sh

    <Port> is 3001.

    Note: supplier1 can only raise an invoice (number 3 below).

10. To test as OEM, open a new Terminal window, type and press Enter: node appOEM.sh

    <Port> is 3002.

    Note: OEM can only set that goods are received (number 4 below).


C. How to use:
	
1. Open Postman

2. To display all invoices, set it to GET, type localhost:3000/invoice the address bar and click Send.

3. To raise an invoice, set it to POST, go to Body tab, and tick x-www-form-urlencoded

   Type in the following keys: (one key per line, case-sensitive)

	     Key			Value (sample)
	
	billedTo		Lenovo
	invoiceDate		2/9/2019
	invoiceAmount		50000
	itemDescription		any description here
	gr			no
	isPaid			no
	paidAmount		0
	repaid			no
	repaymentAmount		0

   Type localhost:3000/invoice in the address bar and click Send.

   (To clarify if you have post successfully do step number 2)

4. To set that goods are received in an invoice, set it to PUT, go to Body tab, and tick x-www-form-urlencoded

   Type in the following keys: (one key per line, case-sensitive)

	     Key			Value (sample)
	
	invoiceNumber		INV002
	gr			yes

   Type localhost:<Port>/invoice in the address bar and click Send.

   Do number 2 to check if it worked.

5. To pay the supplier by bank, set it to PUT, go to Body tab, and tick x-www-form-urlencoded

   Type in the following keys: (one key per line, case-sensitive)

	     Key			Value (sample)
	
	invoiceNumber		INVxxx
	isPaid			yes
	paidAmount		49000 (this must be less than the invoiceAmount)

   Type localhost:<Port>/invoice in the address bar and click Send.

   Do number 2 to check if it worked.

6. To repay the bank by OEM, set it to PUT, go to Body tab, and tick x-www-form-urlencoded

   Type in the following keys: (one key per line, case-sensitive)

	     Key			Value (sample)
	
	invoiceNumber		INVxxx
	repaid			yes
	repaymentAmount		51000 (this must be greater than the paidAmount)

   Type localhost:<Port>/invoice in the address bar and click Send.

   Do number 2 to check if it worked.


D. Troubleshooting

1. In case errors such as "Invalid Smart Contract function" or "chaincode scm not found" appears, try doing any of the following one at a time:

	a. Check if files are put correctly in fabric-samples/fabcar and fabric-samples/chaincode/fabcar/go directories.

	b. Make sure that scm.go is the only content of fabric-samples/chaincode/fabcar/go directory.

	c. If problem still persists, type in the following commands in Terminal...

		docker rm $(docker ps -a | grep scm | awk '{print $1}') -f
		docker rmi $(docker images -a | grep scm | awk '{print $1}') -f

	   Then do numbers 3 to 5 and 9 in B. Set-up instuctions.

	d. If problem still persists, try restarting your machine and do step c.

2. If the error says ".../chaincode/lib/cid" or any directory is missing, try doing these:

	2.1. Open Terminal and go to your home directory. Then enter these commands...

		go get github.com/golang/protobuf/proto
		go get github.com/hyperledger/fabric/common/attrmgr
		go get github.com/hyperledger/fabric/core/chaincode/lib/cid
		go get github.com/pkg/errors

	2.2. Go to your fabric-samples/chaincode directory and create the following directories...

		golang/protobuf/proto
		hyperledger/fabric/common/attrmgr
		hyperledger/fabric/core/chaincode/lib/cid
		pkg/errors

	2.3. Then go to (where your Go directory is located)/go/src/github.com and copy all the contents inside these directories...

		golang/protobuf/proto
		hyperledger/fabric/common/attrmgr
		hyperledger/fabric/core/chaincode/lib/cid
		pkg/errors

	2.4. Then paste the contents to their respective directories you created in step 2.2.
	

# HyperledgerFabric

