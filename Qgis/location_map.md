# **The Importance of the Location Map**

Location maps play a crucial role in the understanding and communication of spatial information. In the past, navigators relied on rudimentary maps which, although simple, helped them avoid setbacks by defining routes and identifying key landmarks. Location, therefore, is the starting point of any significant discovery.

In mineral or environmental research projects, location maps are indispensable. They guide researchers — including geologists, engineers, and geographers — in identifying promising areas, organizing data, and planning field campaigns. A simple location error can compromise the entire investigative process, underscoring the importance of accurate and well-executed initial mapping.

Recently, I was invited to create location maps for an environmental project in Mozambique. Although often seen as a preliminary step, this phase was essential for contextualizing the study area, aligning spatial data with the project’s goals, and facilitating communication among stakeholders. A location map is not merely a visual aid — it is the foundation for any well-informed decision-making process.

For this work, the QGIS platform was fundamental. Its user-friendly and intuitive graphical interface allows for efficient results. Version 3.40.5 was used, and three cartographic products were generated. Figure 1 presents the location and extent of Mozambique, a country located in Southern Africa, highlighting the Mozambican portion of the Umbeluzi River Basin and its spatial configuration.

Southern Africa comprises sixteen countries, including South Africa, Mozambique, and Eswatini. The Umbeluzi River is shared between Mozambique and Eswatini, originating in the latter. It flows through the Lubombo Mountains and drains into Maputo Bay. As a transboundary watercourse, the Umbeluzi presents complex challenges for integrated water resource management.

The boundaries of Mozambique were obtained directly in QGIS using the HCMGIS plugin, which provides GADM data (also available at https://gadm.org
). The background imagery was also acquired using HCMGIS tile map services. The client provided vector data for the regional watersheds as well as a basic hydrography layer.

Once the Umbeluzi Basin had been located at a regional scale (Figure 1), the next objective was to better present its geometry and spatial distribution (Figure 2). The Mozambican segment of the basin is located in Maputo Province and covers an area of 2,272 km². In Eswatini, the basin occupies an additional 3,128 km², totaling 5,400 km². Across the entire basin, seventeen sub-basins were delineated for hydrological and management purposes.

At this stage, the client had a clear understanding of the spatial distribution of the study elements. Confirming that the project is entirely located within Mozambican territory — and that its aim is to investigate how urban expansion has been impacting surface and groundwater — the client requested the identification of three specific sub-basins and the delimitation of a study area at their confluence (Figure 3).

To ensure accuracy in spatial analyses and area calculations, it is essential to use a projection system suited to the study region. Inappropriate projections can cause significant distortions, especially in projects involving watershed area measurements or the delineation of management units. Therefore, the coordinate system UTM Zone 36S (EPSG:32736), based on the WGS 84 datum, was adopted. This system is well-suited for representing southern Mozambique with high precision. Its use ensures that all measurements are consistent with the region’s spatial reality, avoiding errors that could compromise the quality and reliability of the results.
