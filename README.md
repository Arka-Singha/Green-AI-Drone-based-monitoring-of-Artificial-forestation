# 🌿 Green AI – Drone Image Comparison for Afforestation Monitoring

## 📌 Project Overview

**Green AI** is an ML/AI-based framework designed to analyze drone-captured images of afforestation patches. The goal is to **monitor tree growth**, **detect sapling casualties**, and provide a scalable system for evaluating forest health over time.

This project compares orthomosaic drone datasets collected at different time intervals and identifies growth patterns such as:

- 🌱 Growing saplings  
- 🍂 Decaying or diseased trees  
- ❌ Dead saplings (casualties)  

---

## 👤 Team Details

- **Team ID:** 25KTJGREA746575  
- **Member:** Arka Singha  
- **KTJ ID:** 25KTJARK358809  

---

## 🧾 Abstract

This project utilizes Green AI methodologies to analyze drone-captured images of afforestation patches, aiming to detect casualties and monitor tree growth.

Initially, pits of dimension **45×45×45 cm** are identified, and their geo-coordinates are extracted using feature matching from image metadata. Pixel-to-coordinate mapping is performed on orthomosaics, and pit centers are stored in a lookup table.

For subsequent orthomosaics, **3D reconstruction** via **COLMAP** identifies the highest local maxima (tree tips) using pixel-to-height mapping and 8-connectivity searches.

Differences in tree height across orthomosaics are calculated, enabling classification into:

- Positive growth  
- Negative decline  
- Neutral/no change  

Spatial filters, Difference of Gaussians (DoG), and region-growing refine greenery clusters. Advanced segmentation models such as **U-Net** and **DeepLabV3+**, along with vegetation indices (**NDVI, GCI**), provide robust monitoring of forest health.

---

## 🎯 Key Objectives

- Detect sapling casualties in afforestation regions  
- Track tree height progression over time  
- Perform greenery segmentation from soil/background  
- Generate geo-referenced growth reports  
- Support sustainable and scalable forest monitoring  

---

## 🛰️ Workflow Pipeline

---

### ✅ Operation 1 (OP1): Pit Detection & Geo-Mapping

1. Drone images captured → Orthomosaic generation (**Pix4D**)  
2. Detect plantation pits (**45×45×45 cm**)  
3. Extract pit center pixel coordinates  
4. Feature-match metadata to retrieve:

   - Latitude  
   - Longitude  
   - Altitude  

5. Save results into a **Lookup Table**

#### Lookup Table Format

| Grid No. | Center Pixel | Latitude | Longitude | Altitude |
|---------|-------------|----------|----------|----------|
| 1       | (x, y)      | xx.xxxx  | yy.yyyy  | z.zz     |

---

### ✅ Detection with SAM2 Segmentation

To detect saplings precisely:

- Use **SAM2 Semantic Segmentation**
- Extract masks of greenery
- Compute sapling area and pixel clusters
- Add detected saplings into Lookup Table

---

### ✅ Operation 2 (OP2): Tree Tip Detection via 3D Reconstruction

1. Orthomosaic 2 generated  
2. Perform **COLMAP-based 3D photogrammetry**  
3. Identify highest local maxima in Z-axis (tree tip)  
4. Use **8-connectivity search** recursively from pit center  
5. Store updated data:

| Grid No. | Center Pixel | Lat | Long | Alt | TOP Pixel | TOP Z-value |
|---------|-------------|-----|------|-----|----------|------------|
| 1       | (x, y)      | ... | ...  | ... | (x2, y2) | z2         |

---

### ✅ Operation 3 (OP3): Multi-Time Growth Monitoring

Repeat OP2 for Orthomosaic 3 and generate Output 3.

---

## 📊 Growth & Casualty Analysis

### Difference Computation

Tree growth is analyzed using height differences:

- **Difference 1 = Output2 – Output1**
- **Difference 2 = Output3 – Output2**
- **2nd Order Difference** for trend prediction

---

### Interpretation

For each grid:

- **+ve** → Tree growing  
- **-ve** → Tree decaying/dead  
- **0** → No growth or diseased  

---

## 🌿 Individual Tree Health Analysis

To refine greenery evaluation:

### Region Growing Algorithm

- Expand connected green pixels from pit center/tree tip  
- Remove unconnected noise pixels  
- Count green pixels per sapling  

---

### Deep Learning Models Used

- **U-Net**
- **DeepLabV3+**

---

### Vegetation Indices

- **NDVI (Normalized Difference Vegetation Index)**
- **GCI (Green Chlorophyll Index)**

These help measure sapling health dynamically.

---

## 🛠️ Technologies & Tools

| Component | Tools/Models |
|----------|-------------|
| Orthomosaic Generation | Pix4D |
| 3D Reconstruction | COLMAP |
| Segmentation | SAM2, U-Net, DeepLabV3+ |
| Filtering | DoG, Spatial Filters |
| Connectivity Search | 8-Neighbor Traversal |
| Vegetation Health | NDVI, GCI |

---

## 📌 Applications

- Smart afforestation monitoring  
- Forest health surveillance  
- Drone-based environmental AI  
- Sustainable plantation assessment  
- Early detection of sapling mortality  

---

## 📚 References

- UAV-Based Photogrammetry in Forestry  
  https://www.mdpi.com/1999-4907/13/2/173  

- Digital Terrain Modeling & Remote Sensing  
  https://www.mdpi.com/2072-4292/11/11/1271  

---

## 🚀 Future Improvements

- Real-time drone inference pipeline  
- Automated casualty alert system  
- Integration with GIS dashboards  
- Transformer-based vegetation analysis  
- Full deployment as a Green AI monitoring platform  

---

## ⭐ Acknowledgement

This project contributes toward sustainable AI and afforestation monitoring by combining drone photogrammetry, segmentation models, and growth-difference analytics.

---

## 📩 Contact

**Arka Singha**  
KTJ ID: 25KTJARK358809  

---

## 🏆 Achievement

This project was recognized at **Kshitij 2025, IIT Kharagpur**, where it secured:

- 🥉 **3rd Position** in the **Green AI** event  
- Awarded a **Certificate of Merit** for innovation in drone-based afforestation monitoring  

This achievement highlights the impact and potential of the proposed AI-driven framework in sustainable environmental applications.

---
<img width="1102" height="619" alt="image" src="https://github.com/user-attachments/assets/3162cf3b-c09c-4d1a-8714-8345c09f470d" />

