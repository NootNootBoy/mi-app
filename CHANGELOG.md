<!-- Available h3 headings: Added, Fixed, Updated, Removed, Deprecated -->

# Changelog

All notable changes to this template will be documented in this file.

## v1.2.0 (2023-03-20)

### Added

- Added .gitattributes file
- Added Progress component page
- Added necessary props for the UserLayout
- Added custom variable `avatarBg` for Avatar background-color in the MUI's palette
- Added ability to access vertical or horizontal layout with menu without logging in
- Added articles on how to migrate from JWT Auth to [NextAuth](https://next-auth.js.org/), NextAuth with [CredentialsProvider](https://next-auth.js.org/configuration/providers/credentials) and NextAuth with [GoogleProvider](https://next-auth.js.org/providers/google) & [PrismaAdapter](https://next-auth.js.org/adapters/prisma)

### Updated

- Updated docs
- Updated FAQs on the Pricing page
- Changed MUI Links to Next.js Links
- Updated examples on the Dialog pages
- Updated `trackBg` colors in the theme
- Changed method of implementing semi-dark skin
- Updated input mask labels on the Input Mask page
- Updated bg-colors of social cards on the Card Basic page
- Updated MUI's theme structure which is in the `src/@core` folder
- Update `lang` attribute on the `<html>` tag when the language is changed
- Updated structure of points in the Knowledge Base section on the Help Center page
- Updated UI of avatar, breadcrumb, chip, dataGrid, list, tooltip, snackbar, switch components
- Updated all the packages (Refer to the official docs for the migration of `@mui/x-data-grid` from [here](https://mui.com/x/migration/migration-data-grid-v5/))

### Fixed

- Fixed types
- Fixed vertical menu re-renders on hover
- Fixed transition issue on pull-up Avatars
- Fixed Alert snackbar shadow in bordered skin
- Fixed shadows in the whole template when the skin is semi-dark
- Fixed `react-hot-toast`'s z-index when its position is on the left side
- Fixed shadow between nav header and nav items in the Vertical navigation menu in RTL
- Fixed bugs in the Chat, Calendar, Invoice, User apps and User Profile, FAQ, File Uploader pages

### Removed

- Removed unnecessary images
- Removed validation on the Register page
- Removed all the files and guides related to Firebase (in favour of NextAuth)

## v1.1.0 (2022-11-16)

### Added

- Added `.vscode` folder in all the `full-version` and `starter-kit` folders

### Updated

- Updated docs
- Updated Next.js to v13
- Optimized all the images
- Moved JWT configs to the `.env` file
- Updated spacing in the `Button` component
- Updated all the dependencies to the latest versions
- Updated all the MUI links (with `href='/'`) to Next.js links

### Fixed

- Fixed minor bugs
- Fixed border-right in the Calendar app
- Fixed console error on the Help Center page
- Fixed scroll issue when page loader renders
- Fixed spacing in the left sidebar in the Email app
- Fixed z-index of `react-hot-toast` in smaller screens
- Fixed a few re-renders in the Vertical navigation menu
- Fixed types in `UserLayout` component and custom components inside the `src/@core` folder

### Removed

- Removed validations from some pages

## v1.0.0 (2022-10-13)

### Added

- Initial Release
