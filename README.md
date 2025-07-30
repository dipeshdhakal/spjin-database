# 🗄️ SPJIN Database Releases

This repository contains encrypted database releases for the SPJIN app. Users can download database updates automatically through the app, while maintaining security through encryption.

## 🚀 For Publishers (You)

### Quick Update Process

1. **Create a new branch**: `feat/update`
2. **Compress your raw database file** and add it to the `/database` directory
3. **Push to GitHub**: The workflow automatically extracts, encrypts, creates a release, and cleans up!

### Step-by-Step Instructions

```bash
# 1. Create and switch to update branch
git checkout -b feat/update

# 2. Compress your database file (recommended for large files)
zip database/SPJIN.db.zip /path/to/your/SPJIN.db

# Alternative: Copy uncompressed file directly
# cp /path/to/your/SPJIN.db database/

# 3. Commit and push
git add database/
git commit -m "Update database with new content"
git push origin feat/update

# 4. That's it! GitHub Actions handles the rest automatically
```

### What Happens Automatically

When you push to `feat/update`:
- 📦 **Extracts** compressed database (if you uploaded a .zip file)
- ✅ **Validates** your database file
- 🔐 **Encrypts** it with AES-256-CBC
- 📊 **Increments** the major version number automatically
- 🔄 **Updates** the main branch with the encrypted database
- 🚀 **Creates** a new GitHub release with the encrypted file
- 🗑️ **Deletes** the `feat/update` branch to keep things clean

## 🔐 Security Features

- ✅ **Encrypted Storage**: All databases encrypted with AES-256-CBC
- ✅ **Access Control**: Only repository collaborators can publish
- ✅ **Automatic Validation**: Database structure validation before release
- ✅ **Major Versioning**: Each update creates a new major version for clear tracking

## 📱 For App Users

Database updates are automatic:
- App downloads encrypted database from GitHub releases
- App automatically decrypts using the configured key
- Users see progress during download
- No manual intervention required

## 📊 Release Information

Each release includes:
- Encrypted database file ready for mobile app download
- Detailed changelog with update information
- File size and metadata
- Automatic major version increment

## 🔍 Repository Structure

```
spjin-database/
├── database/           # Your source database files
│   ├── SPJIN.db       # Raw database file (option 1)
│   └── SPJIN.db.zip   # Compressed database (option 2, recommended for large files)
├── .github/
│   └── workflows/
│       └── auto-release.yml  # Automation workflow
└── README.md          # This file
```

## 🛠️ Setup Instructions

### First Time Setup

1. **Clone this repository**:
   ```bash
   git clone https://github.com/dipeshdhakal/spjin-database.git
   cd spjin-database
   ```

2. **Configure your encryption key** (GitHub repository settings):
   - Go to Settings → Secrets and variables → Actions
   - Add secret: `DB_ENCRYPTION_KEY` with your encryption password
   - Use a strong password (recommended: 32+ characters)

3. **Update your app configuration**:
   ```kotlin
   githubRepo = "dipeshdhakal/spjin-database"
   ```

### Regular Usage

Simply create a `feat/update` branch and add your database:

```bash
# Create update branch
git checkout -b feat/update

# Option 1: Add compressed database (recommended for large files)
zip database/SPJIN.db.zip /path/to/your/SPJIN.db

# Option 2: Add raw database file directly
# cp /path/to/your/SPJIN.db database/

# Commit and push
git add database/
git commit -m "Update database with new content"
git push origin feat/update

# The workflow handles everything else automatically!
```

## 📈 Monitoring

- **GitHub Actions**: Monitor workflow runs in the Actions tab
- **Releases**: View all releases and download statistics
- **Analytics**: Track download patterns and user adoption

## 🆘 Troubleshooting

### Common Issues

**"No database file (.db or .zip) found in /database directory!"**
- Make sure your database file is in the `database/` folder
- Ensure the file has a `.db` extension (or is inside a `.zip` file)
- For large files, compress them first: `zip database/SPJIN.db.zip /path/to/SPJIN.db`

**"No .db file found inside the zip archive!"**
- Check that your zip file contains a `.db` file
- Ensure the database file has the correct extension

**"Database file is empty"**
- Check that your database file is a valid SQLite database
- Ensure the file was copied/compressed correctly

**Workflow fails on GitHub**
- Check that `DB_ENCRYPTION_KEY` secret is set correctly
- Verify the database file was committed to the `feat/update` branch
- Check the Actions tab for detailed error logs

**App can't download updates**
- Ensure repository is public
- Check that releases are being created successfully
- Verify app has correct repository configuration

### Getting Help

- Check the **Actions** tab for detailed workflow logs
- Ensure your database follows the expected schema
- Verify encryption key is set in repository secrets

## 🎯 Best Practices

- **Test databases** thoroughly before pushing to `feat/update`
- **Use clear commit messages** to help track changes
- **Keep backups** of your database files
- **Monitor the Actions tab** to ensure workflows complete successfully
- **Only push raw database files** to the `feat/update` branch (encryption is automatic)

---

This automated system ensures your SPJIN app users always have the latest content while maintaining complete security and control over releases! 🎉
