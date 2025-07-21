# Operations/Production - NIHMS Credentials Configuration

The NIH Manuscript Submission (NIHMS) system provides a way to get manuscripts into Pub Med Central (PMC). Refer to 
the [NIHMS documentation](https://www.nihms.nih.gov/about/overview/) for the details about how it works.  

PASS provides functionality to assist in making manuscript deposits into PMC.  However, it is important to know that 
there are a number of the manual steps in the NIHMS workflow that occur after PASS completes a deposit.  People examine 
the submission, put in metadata, and approve some of the steps. And in fact a PI is required to log into NIHMS in order 
to approve the submission.

The following sections describe the PASS components that interact with NIHMS/PMC along with required credentials.

## PASS NIHMS Deposit

PASS uses the NIHMS Publisher Bulk-Upload protocol which was designed for the use of publishers. The PASS deposit 
service produces a package and uploads it to an SFTP server controlled by NIH. Then the package starts going through 
the NIHMS workflow steps. If all goes well, a PASS deposit starts out at step 2.

### SFTP server credentials

Review the information on this page about the [NIHMS Publisher Bulk-Upload](https://support.nlm.nih.gov/kbArticle/?pn=KA-05267) 
protocol, and then contact the [NIHMS Help Desk](mailto:nihms-help@ncbi.nlm.nih.gov) to obtain the credentials. This 
process will result in credentials to authenticate with the SFTP server as well as a set of credentials to log into
NIHMS for monitoring deposits made with PASS.

## NIHMS Deposit Email Monitor

Some information is communicated back from NIHMS through email. The PASS deposit service can monitor that email to 
update the deposit status. See the [configuration documentation](../../developer-documentation/deposit-service/ds-configuration.md#configuring-the-nihms-email-service) 
for how to set the NIHMS Email configuration.

### NIHMS Email Monitor credentials

The email address that receives the emails from NIHMS is the email of the user created to log into NIHMS obtained as 
part of the Publisher Bulk-Upload process described above.

## NIHMS Data Loader

The NIHMS data loader checks PMC submissions and updates PASS submissions with assigned PMC IDs when appropriate. This 
requires an NIH Public Access Compliance Monitor (PACM) API token.

### NIHMS Data Loader API Token

An NIH/ERA account must be created to obtain the PACM API token. See this page for instructions: [PACM API Token](./ops-loaders.md#pacm-api-token)

The API token can be manually retrieved from [PACM website](https://www.ncbi.nlm.nih.gov/pmc/utils/pacm).  The token is 
valid for three months and there is currently no way to automatically refresh the token through PACM.  PASS does provide
an option to automatically refresh the token using the NIHMS API Token Refresh Automation container.

## NIHMS Troubleshooting

In order to answer questions from people that used PASS to perform a NIHMS deposit, it is useful to know how to log 
into NIHMS to see the deposit and what state it is in within the NIHMS workflow. This can be accomplished by using the 
NIHMS credentials to log into [NIHMS](https://www.nihms.nih.gov/login/?next=/submission/) to see all NIHMS deposits 
made through your institution's PASS system.
