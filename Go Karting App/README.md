# A Square Go Karting

## Table of Contents

- [Project Overview](#1-project-overview)
- [My Role](#my-role)
- [Key Features](#2-key-features)
- [Tech Stack](#3-tech-stack)
- [Screenshots](#4-screenshots)
- [Notes](#5-notes)

## 1. Project Overview

A Square Go Karting is a comprehensive Flutter mobile application designed to streamline the entertainment experience for go-karting enthusiasts. The platform serves as a unified booking and management hub where users can discover activities, book sessions for go-karting and related entertainment, and handle payments within a single, polished interface.

The application bridges the gap between physical entertainment venues and digital convenience, providing a seamless flow from activity discovery to ticket generation. It handles complex workflows such as real-time session booking, coupon management, and secure third-party payment integration, ensuring a reliable experience for the end user.

## My Role

I was responsible for the **modernization, stabilization, and release engineering** of the application. My work focused on bringing an existing codebase up to production standards and ensuring compatibility with the latest mobile ecosystems.

My contributions included:

- **Framework Modernization**: Migrated the entire project to a modern Flutter and Dart SDK baseline, resolving numerous breaking changes and deprecated API usages.
- **Dependency Management**: Audited and upgraded the project's dependency tree to ensure stability, security, and compatibility with current Android and iOS toolchains.
- **Platform Re-engineering**: Rebuilt the Android and iOS project configurations from the ground up to support modern build systems, permissions, and platform-specific requirements.
- **Infrastructure Migration**: Orchestrated the migration of the application to a new Firebase project, updating all platform-specific configuration files and authentication flows.
- **UI/UX Optimization**: Fixed critical UI/UX inconsistencies across multiple screens to provide a more fluid and professional user experience.
- **Stability and Performance**: Improved runtime stability by resolving legacy bugs and optimizing the application's response to network and state changes.

## 2. Key Features

- **Authentication & Onboarding**: Implemented a secure mobile number-based login flow with OTP verification and a customized splash screen experience.
- **Activity Discovery**: Built a dynamic home dashboard featuring promotional banners, searchable activity lists, and categorized entertainment options.
- **Comprehensive Booking Flow**: Designed an end-to-end booking journey including cart management, session overview, and order confirmation.
- **Rewards & Discounts**: Integrated coupon handling and in-app rewards (e.g., tyre discounts) to drive user engagement during the booking process.
- **Secure Payments**: Integrated the Razorpay Flutter SDK for reliable and secure online payment processing.
- **Digital Ticketing**: Developed a post-booking flow that generates downloadable and shareable tickets with QR/order tracking capabilities.
- **Real-time Notifications**: Integrated Firebase Cloud Messaging (FCM) for push notifications to keep users updated on bookings and promotions.
- **Media Integration**: Integrated YouTube playback for a rich video feed experience within the app browsing flow.
- **Social Growth**: Implemented referral and sharing mechanisms to support organic user acquisition.

## 3. Tech Stack

### Frontend & State Management
- **Flutter (Dart)**: For cross-platform mobile development.
- **Provider**: Utilized for predictable and efficient state management.
- **MVC Pattern**: Structured the codebase using a Model-View-Controller architecture for better separation of concerns.

### Backend & Infrastructure
- **Firebase Core**: For centralized app configuration.
- **Firebase Authentication**: Handling secure OTP-based user sessions.
- **Firebase Cloud Messaging**: For reliable push notification delivery.
- **REST APIs**: Consuming backend services for booking and activity data.

### Integrations & Utilities
- **Razorpay SDK**: For secure payment gateway integration.
- **YouTube Player**: For seamless video content delivery.
- **Shared Preferences**: For lightweight local data persistence.
- **Share Plus & Screenshot**: For ticket sharing and social features.

## 4. 📸 Screenshots

<div align="center">
  <table style="width: 100%; border-collapse: collapse;">
    <tr>
      <td width="33.33%" align="center">
        <img src="screenshots/Home.jpg" width="90%" alt="Home"/><br/>
        <b>Home</b>
      </td>
      <td width="33.33%" align="center">
        <img src="screenshots/Cart.jpg" width="90%" alt="Cart"/><br/>
        <b>Cart</b>
      </td>
      <td width="33.33%" align="center">
        <img src="screenshots/Order_Review.jpg" width="90%" alt="Order Review"/><br/>
        <b>Order Review</b>
      </td>
    </tr>
  </table>
</div>

For a full view of all application screens including the splash screen, notifications, and settings, please visit the [Screenshots Gallery](./screenshots/README.md).

## 5. Notes

- This project was originally developed earlier; my role was specifically focused on **modernization, platform upgrades, and production stabilization**.
- I successfully transitioned the project from a legacy state to a production-ready application capable of running on the latest versions of Android and iOS.
- Core business logic and initial payment integrations were preserved while platform-level infrastructure (Firebase, SDKs, build scripts) was completely overhauled.
