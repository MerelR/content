# Cloud Application
Version 7 offers variaDoc as a cloud application or Software as a Service (SaaS). The cloud application runs on a reliable cloud infrastructure. It is delivered through the web browser and does not require any downloads or installations on the client side.

## Compare to Desktop Application 

The cloud application looks almost exactly as the desktop application. It differs as follows:

- projects are saved automatically
- you may save and retrieve labeled revision
- instead of activating a serial, your license status is part of your account
- your account has an online disk
- projects can be turned into a web API
- you may access external cloud storage such as Google Drive

## Get started
To get started, register an account if you don't have one yet. Next, login and navigate to [app.variadoc.com](app.variadoc.com). From here on, things should be fairly self-explanatory.

You will notice that initially your online disk has a folder `/samples`. Next open project `/samples/authors/authors.vd` by clicking the file.

The project editor will start and look as follows:

[picture]

Hit the Merge button from the toolbar. You will find the generated documents inside `/samples/authors/out`.

## Online disk
Each variaDoc account has an online disk. This disk is accessible from every project inside your account and files can be shared among online variaDoc projects. In fact, every project is a .vd file on this disk. How you organize your folders and files is entirely up to you.

Files on your online disk are referenced like this: `~/samples/authors/template.pdf`.

### Backup
You can download a copy of your online disk at any moment. You may also schedule a regular backup.

## Cloud storage 
Files in your cloud storage are referenced like this: `@documents/authors/template.pdf`. `documents` is the alias of a configured cloud storage folder.

## Cloud license
The variaDoc cloud application offers three tiers: 

- Free
- Professional
- Enterprise

### Free

The Free tier is limited to a single variaDoc project. Document generation is limited to *N* pages per month. The online disk has a capacity of *X* GB. Use of external cloud storage is unlimited. All PDF output has a watermark.

This tier is suitable for evaluation. 

After registering a variaDoc account for the first time, you are automatically on the Free tier.

### Professional
The Professional tier allows unlimited projects. Document generation is limited to *K* pages per month. The price of each addtional page is *k*. The online disk has a capacity of *Y* GB. Use of external cloud storage is unlimited.

This tier is suitable for one-man shops.

### Enterprise (coming soon)
In addition to the Professional tier, the Enterprise tier introduces *teams*. A team has on online disk that can be accessed from member accounts. This allows sharing templates, assets, data and generated output.

The account that is on the Enterprise tier manages the team and access to the shared disk.

Files on the team disk are referenced like this: `~~/samples/authors/template.pdf`.

### Anynomous
All previous tiers require you to register an account. It is also possible to use the cloud application anonymously. In this case a temporary storage area will be created for the duration of your session. Limitations:

- all PDF output has an evaluation watermark
- access to cloud storage cannot be configured
- storage is limited to *Z* Mb

The table below summarizes the tiers and anonymous use:

|            |projects |pages/month  |storage|external storage|web api|teams|
|------------|---------|-------------|-------|----------------|-------|-----|
|Enterprise  |unlimited|             |5+5 GB |unlimited       |Yes    |Yes  |
|Professional|unlimited|             |5 GB   |unlimited       |Yes    |No   |
|Free        |1        |100          |100 MB |unlimited       |No     |No   |
|Anonymous   |1        |             |10 MB  |No              |No     |No   |

*) 1 USD per 100 pages
