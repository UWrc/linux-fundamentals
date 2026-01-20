# Data Transfer: Moving Files To and From Hyak Klone a& Tillicum

Efficient and reliable data transfer is a key part of working on Klone and Tillicum. There are two main ways to move files between your local computer and the cluster:

| Method                           | Best For                               | Notes                                                                            |
| -------------------------------- | -------------------------------------- | -------------------------------------------------------------------------------- |
| **`scp` (Secure Copy Protocol)** | Small to medium file transfers         | Simple and available by default on all systems                                   |
| **Globus**                       | Large datasets, unsupervised transfers | Automatically handles restarts and failures, ideal for long or complex transfers |

## Transfer Data with `scp`

`scp` (secure copy) works similarly to `ssh`. You’ll use your UW NetID credentials to securely copy data between your local machine and Klone or Tillicum.

> **NOTE: These commands must be run from your local terminal, not from inside the cluster.**

### Upload files from your local computer to Klone

```bash 
scp data_to_transfer UWNetID@klone.hyak.uw.edu:/gscratch/scrubbed/UWNetID
```
Replace `UWNetID` with your UW NetID in both the login and path.

### Download files from Klone to your local computer

```bash
scp UWNetID@klone.hyak.uw.edu:/gscratch/scrubbed/UWNetID/linux-fundamentals/example.sh .
```
The `.` at the end of the command tells `scp` to place the files in your current working directory or "here."

## Transfer Data with Globus

While `scp` is great for quick transfers, **Globus** is the best way to move large datasets reliably and automatically.

Globus provides:
* **Automatic checkpointing** – transfers resume if your connection drops
* **Integrity checks** – ensures every file arrives intact
* **Unsupervised transfers** – no need to remain logged in

Globus is available on Hyak Klone, Tillicum, Kopah, and UW OneDrive, allowing for seamless and high-speed data transfers between endpoints.

Here we will demonstrate data transfers with Globus on Hyak Klone. [Equivalent Globus instructions for Tillicum](https://github.com/UWrc/tillicum-onboarding/blob/main/04-file-transfer.md#transfer-data-with-globus).

> **NOTE: Sharing not Enabled**
>
> Globus public sharing is not yet enabled on Klone or Tillicum. 
> 
> Globus public sharing is available with [**<ins>Kopah S3 storage</ins>**](https://hyak.uw.edu/docs/storage/gui#globus), which we recommend as a compliment for your research storage portfolio if you anticipate regular external sharing and collaboration.

## Getting Started

1. Go to **<ins>https://www.globus.org</ins>** and Log In using University of Washington as your organization.

![Screenshot of globus.org showing the login button in the upper right corner.](/img/globus_login.png 'globus')

*Screenshot of globus.org showing the login button in the upper right corner.*

2. Sign in with your UW NetID and complete Duo 2FA.
3. Open the File Manager and search for the collection: **UW Hyak Klone**

![Screenshot showing how to search for the Klone endpoint.](/img/find_collection.png 'Klone endpoint')

*Screenshot showing how to search for the Klone endpoint.*

4. Bookmark this collection so you can easily access it later.

![Screenshot showing how to bookmark the Klone endpoint.](/img/bookmark.png 'bookmark')

*Screenshot showing how to bookmark the Klone endpoint.*

The directory `/mmfs1` will be the default path when you connect.

5. Navigate to your working directory by selecting `/mmfs1/` by double clicking it, then selecting `scubbed/`, then your working directory, which should be you UWNetID, and then the git hub repository directory `linux-fundamentals/`. 

![Screenshot showing the git hub repository directory and the Klone path on Globus.](/img/globus_path.png 'path')
*Screenshot showing the git hub repository directory and the Klone path on Globus.*

This navigation can also be done by typing the path into the Path field, `/gpfs/scrubbed/UWNetID/tillicum-onboarding` after replacing the word UWNetID with your UW NetID. 

## Set Up Your Local Endpoint

To transfer data between your computer and Klone, you’ll need to install Globus Connect Personal:

1. [**<ins>Download Globus Connect Personal</ins>**](https://www.globus.org/globus-connect-personal) for your operating system.
2. Follow the on-screen setup to name your computer (e.g., User-MacBook-Pro or Lab-Desktop).
3. Once configured, your computer becomes a personal endpoint in Globus. You can find it by searching your chosen name under Collections.

![Screenshot showing the result of setting up Globus Connect Personal properly.](/img/gcp_endpoint.png 'personal endpoint')
*Screenshot showing the result of setting up Globus Connect Personal properly.*

4. Bookmark your the collection representing your Globus Connect Personal for quick access later. 

## Practice Transfers

Globus has a two-pane view option which can allow you to see two collections in the same window and perform transfers between them. We’ll use the files in this training repository to practice moving data both ways.

1. In one panel of the Globus File Manager, open UW Hyak Klone.
2. In the other panel, open your personal endpoint (your local computer).

#### Try:
1. Transferring a file from **Klone → Local**. The image below shows the two pane view with Klone on the right and your local collection on the left. Select one of the files from the `linux-fundamentals` repository to transfer and click start. You will see a green status box and detailed transfer steps can be viewed. A email will be sent to you when the transfer is completed. 

![Screenshot showing the 2-pane view set up with local and Klone collections, the button to start the transfer, the transfer status box, and the checkbox of file selected to transfer.](/img/transfer_to_local.png 'transfer')
*Screenshot showing the 2-pane view set up with local and Klone collections, the button to start the transfer, the transfer status box, and the checkbox of file selected to transfer.*

2. Transferring a file from **Local → Klone**. Repeat the same steps but in the opposite direction. **Uncheck the file on the Klone side**, this is required to send files the other way. On the Local side, check the box next to any file and click start to begin the transfer to Klone. 

![Screenshot showing the 2-pane view set up with local and Klone collections, the button to start the transfer, the transfer status box, and the checkbox of file selected to transfer.](/img/transfer_from_local.png 'transfer again')
*Screenshot showing the 2-pane view set up with local and Klone collections and key buttons for starting a transfer.*

Globus will display progress in real time, and you’ll receive an email once the transfer is complete.

## OneDrive Connector 

We’re excited to announce our Microsoft OneDrive connector for Globus, allowing you to move files directly between OneDrive and Hyak Klone.

💡 Did you know? UW community members receive 5 TB of storage on OneDrive as part of Microsoft 365. [**<ins>Learn more here.</ins>**](https://uwconnect.uw.edu/it?id=kb_article_view&sysparm_article=KB0034422)

Search for **UW OneDrive** and bookmark it for easy access.

![Screenshot showing the Uw OneDrive endpoint in Globus.](/img/onedrive_globus.png 'onedrive')
*Screenshot showing the Uw OneDrive endpoint in Globus.*

![Screenshot showing 2-pane view set up with OneDrive and Klone collections, the button to start the transfer, and the checkbox of file selected to transfer.](/img/onedrive_transfer.png 'onedrive')
*Screenshot showing 2-pane view set up with OneDrive and Klone collections, the button to start the transfer, and the checkbox of file selected to transfer.*

## Learn More

* Globus User Documentation [**<ins>Learn more here.</ins>**](https://docs.globus.org/?_gl=1*s0ry7u*_ga*MTE2MzI4NzMxNi4xNzQyMzQxMTg3*_ga_7ZB89HGG0P*MTc0NDA3MjY1Ny4xNy4xLjE3NDQwNzI2NTcuMC4wLjA.)
* [**<ins>Video Tutorial: Introduction to Globus for Researchers and New Users</ins>**](https://www.youtube.com/watch?v=-j7Mp3FN1zo&list=PLLCSx-IFoBeu2F-HF-DMoc5_AUsvYft8c&index=2)
* [**<ins>Video Tutorial: Globus Connect Personal Setup</ins>**](https://www.youtube.com/watch?v=bpnVcAN99WY). *Note: the Endpoints Menu Tool appears to be deprecated and now "Endpoint" and "Collection" are synonymous. Your personal endpoint can be found by searching Collections.*