# Making Your Locally Hosted Static Website Accessible through AWS Cloud

To make your locally hosted static website accessible to the public through the AWS cloud, follow these detailed steps:

1. **Set up Amazon S3**: Amazon S3 (Simple Storage Service) will be used to host your static website files. Follow these steps:

   - Log in to the AWS Management Console.
   - Open the Amazon S3 service.
   - Click on "Create bucket" to create a new bucket.
   - Provide a unique bucket name and choose the region closest to your target audience.
   - Disable block all public access and acknowledge the settings.
   - Enable static website hosting by going to the bucket properties and enabling it under the "Static website hosting" section.
   - Enter the index document name (e.g., `index.html`) and error document name if applicable.
   - Save the changes.

2. **Upload your website files to Amazon S3**:
   - Select your newly created bucket and choose the "Upload" option.
   - Add your website files to the bucket, including HTML, CSS, JavaScript, images, and any other assets.
   - Make sure to set the appropriate permissions on your files so that they can be publicly accessed.

3. **Configure DNS for your website**:
   - Go to the AWS Management Console and open the Route 53 service.
   - Choose "Hosted zones" and click on "Create hosted zone."
   - Enter your domain name and click "Create."
   - Note down the four nameservers provided by Route 53.

4. **Update DNS settings with your domain registrar**:
   - Log in to your domain registrar's website where you purchased the domain.
   - Locate the DNS management section and update the nameservers with the ones provided by Route 53.
   - Save the changes. Note that DNS propagation may take some time, typically a few hours, before your domain points to Route 53.

5. **Set up an Amazon CloudFront distribution**:
   - Go to the AWS Management Console and open the CloudFront service.
   - Click on "Create Distribution" and choose the Web delivery method.
   - Configure the following settings:
     - In the "Origin Settings," select your S3 bucket as the origin domain name.
     - Enable the option to Restrict Bucket Access.
     - In the "Default Cache Behavior Settings," choose "Redirect HTTP to HTTPS."
     - Configure any additional settings as per your requirements.
     - Save the changes.

6. **Associate your CloudFront distribution with your domain**:
   - Once the CloudFront distribution is created, note down the CloudFront domain name.
   - Go back to the Route 53 service in the AWS Management Console.
   - Choose the hosted zone for your domain and click "Create Record Set."
   - Create a new record set with the following details:
     - Set the record name (e.g., `www`) or leave it blank for the root domain.
     - Select "A - IPv4 address" for the record type.
     - Choose "Yes" for "Alias."
     - In the "Alias Target," enter the CloudFront domain name.
     - Save the changes.

7. **Test and verify**:
   - Wait for the DNS propagation to complete (up to 24 hours).
   - Visit your website by entering your domain name (e.g., `www.yourdomain.com`) in a web browser.
   - Ensure that your website loads correctly and all the links, images, and assets are accessible.
