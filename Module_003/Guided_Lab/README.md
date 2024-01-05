# Module 3 - Guided Lab: Hosting a Static Website

## Lab overview and objectives

Static websites have fixed content with no backend processing. They can contain HTML pages, images, style sheets, and all files that are needed to render a website. However, static websites do not use server-side scripting or a database. If you want your static webpages to provide interactivity and run programming logic, you can use JavaScript that runs in the user's web browser.

You can easily host a static website on Amazon Simple Storage Service (Amazon S3) by uploading the content and making it publicly accessible. No servers are needed, and you can use Amazon S3 to store and retrieve any amount of data at any time, from anywhere on the web.

After completing this lab, you should be able to:
- Create a bucket in Amazon S3
- Upload content to your bucket
- Enable access to the bucket objects
- Update the website

## Task 1: Creating a bucket in Amazon S3

In this task, you will create an S3 bucket and configure it for static website hosting.

1. In the `AWS Management Console`, on the `Services` menu, choose `S3`.
2. Choose `Create bucket`. 

    An S3 bucket name is globally unique, and the namespace is shared by all AWS accounts. After you create a bucket, the name of that bucket cannot be used by another AWS account in any AWS Region unless you delete the bucket.

    Thus, for this lab, you will use a bucket name that includes a random number, such as: website-123

3. For `Bucket name`, enter: website-<123> (replace <123> with a random number)

    Public access to buckets is blocked by default. Because the files in your static website will need to be accessible through the internet, you must permit public access.

    Verify the AWS Region is set to us-east-1 (if it is not, choose the us-east-1 Region)

4. In the Object Ownership section, select ACLs enabled, then verify Bucket owner preferred is selected.

5. Clear Block all public access, then select the box that states I acknowledge that the current settings may result in this bucket and the objects within becoming public.

6. Choose `Create bucket`.

    You can use tags to add additional information to a bucket, such as a project code, cost center, or owner.

7. Choose the name of your new bucket.
8. Choose the  Properties tab.
9. Scroll to the Tags panel.
10. Choose Edit then Add tag and enter:

    Key: Department\
    Value: Marketing

11. Choose Save changes to save the tag.

    Next, you will configure the bucket for static website hosting.

12. Stay in the Properties console.
13. Scroll to the Static website hosting panel.
14. Choose Edit

15. Configure the following settings:

    `Static web hosting`: Enable

    `Hosting type`: Host a static website

    `Index document`: index.html

    Note: You must enter this value, even though it is already displayed.
    Error document: error.html

16. Choose `Save changes`

17. In the Static website hosting panel, choose the link under Bucket website endpoint.

    You will receive a 403 Forbidden message because the bucket permissions have not been configured yet. Keep this tab open in your web browser so that you can return to it later.

    Your bucket has now been configured to host a static website.


## Task 2: Uploading content to your bucket

In this task, you will upload the files that will serve as your static website to the bucket.

1. Download the files index.html, script.js and style.css
2. Return to the Amazon S3 console and in the website-<123> bucket you created earlier, choose the Objects tab.

3. Choose Upload

4. Choose Add files

5. Locate and select the three files that you downloaded.

6. If prompted, choose I acknowledge that existing objects with the same name will be overwritten.

7. Choose Upload

    Your files are uploaded to the bucket.

    Choose Close


## Task 3: Enabling access to the objects

Objects that are stored in Amazon S3 are private by default. This ensures that your organization's data remains secure.

In this task, you will make the uploaded objects publicly accessible.

First, confirm that the objects are currently private.

1. Return to the browser tab that showed the 403 Forbidden message.

2. Refresh the webpage.

    If you accidentally closed this tab, go to the Properties tab, and in the Static website hosting panel choose the Endpoint link again.

    You should still see a 403 Forbidden message. 

    Analysis: This response is expected! This message indicates that your static website is being hosted by Amazon S3, but that the content is private.

    You can make Amazon S3 objects public through two different ways:

    - To make either a whole bucket public, or a specific directory in a bucket public, use a bucket policy.
    - To make individual objects in a bucket public, use an access control list (ACL).

    It is normally safer to make individual objects public because this avoids accidentally making other objects public. However, if you know that the entire bucket contains no sensitive information, you can use a bucket policy.

    You will now configure the individual objects to be publicly accessible.

3. Return to the web browser tab with the Amazon S3 console (but do not close the website tab).

4. Select all three objects.

5. In the Actions menu, choose Make public via ACL.

6. A list of the three objects is displayed.

7. Choose Make public
    
    Your static website is now publicly accessible

8. Return to the web browser tab that has the 403 Forbidden message.

9. Refresh the webpage.

   You should now see the static website that is being hosted by Amazon S3.


## Task 4: Updating the website

You can change the website by editing the HTML file and uploading it again to the S3 bucket.

Amazon S3 is an object storage service, so you must upload the whole file. This action replaces the existing object in your bucket. You cannot edit the contents of an object—instead, the whole object must be replaced.

1. On your computer, load the index.html file into a text editor (for example, Notepad or TextEdit).

2. Find the text Served from Amazon S3 and replace it with Created by <YOUR-NAME>, substituting your name for <YOUR-NAME> (for example, Created by Jane).

3. Save the file.

4. Return to the Amazon S3 console and upload the index.html file that you just edited.

5. Select index.html and use the Actions menu to choose the Make public via ACL option again.

6. Return to the web browser tab with the static website and refresh the page.

7. Your name should now be on the page.

Your static website is now accessible on the internet. Because it is hosted on Amazon S3, the website has high availability and can serve high volumes of traffic without using any servers.

You can also use your own domain name to direct users to a static website that is hosted on Amazon S3. To accomplish this, you could use the Amazon Route 53 Domain Name System (DNS) service in combination with Amazon S3.