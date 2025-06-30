This project shows all the current available units from the real estate company Port Property and their locations, prices, types, dates, and photos.
This is intended to make the process of finding an apartment more intuitive to the user while allowing them to more easily find an apartment in a certain area.



If you are an employee in charge of maintaining this map, refer to the text below:

- Adding a new town tab:
    If the company has available units in a town that doesn't have a tab:
    1.  Open mapsearch.html and find <div class="tab-container"> using ctrl+f
        Below should be all the existing tabs, copy any of them and paste it at the end of the tab list, for example 
        <div id="Portland" class="tab tab-portland" data-lat="43.6557" data-lng="-70.2671" data-zoom="14" data-bounds="">Portland</div>
            ^internal id  ^custom appearance       ^latitude          ^longitude          ^initial zoom  ^don't change ^how town name appears on tab
        Change each instance of a town name to the new town to be added (id="Portland" -> NewTown, tab-portland -> tab-newtown, >Portland< -> >NewTown<)
        Also, change the data-lat (latitude) and data-lng (longitude) to match the center of the new town. If it is too zoomed in or zoomed out initially,
        change data-zoom (higher zoom number is more zoomed in)
        Now, there should be a working tab for the new town. Don't worry about spacing, it will happen automatically. 
    2.  Now, search for .tab-portland using ctrl+f and copy and paste it at the end of the .tab-town list. This is for individual customization of the tabs
        Change the name to tab-newtown with newtown being the town to be added
        Also, change the color of the shadow to something that fits the town:
            box-shadow: 0px 0px 1px rgb(0, 90, 207) 
        You can use an online rgb picker and copy the values in. Here's a good one https://www.w3schools.com/colors/colors_picker.asp
        The rest of the code can stay the same, unless you want other customization
    3.  You will also want to add a new town limites polygon to show then the town is selected.
        If the town is in Maine, use this website: https://maine.hub.arcgis.com/datasets/maine::maine-town-and-townships-boundary-polygons-feature-1/explore
        Select the "Filter Data" button (shaped like a filter) and select "TOWN", then search for the town and you should see an outline for only that town.
        Scroll down to the "LAND" filter and select "y". This excludes the ocean in the polygons.
        Then, right below the filters button, there should be a download button. Choose the option for GeoJSON.
        When the file is downloaded, rename it to the town name without spaces, and move it into the boundaries folder in this project.
        Next, use ctrl+f to find fetch('boundaries/portland.geojson') and copy the whole thing (or copy below). It should look like below:
        // Portland city boundaries polygon
        fetch('boundaries/portland.geojson')
        .then(res => res.json())
        .then(geojson => {
            const boundaryLayer = L.geoJSON(geojson, {
            style: { color: 'blue', opacity: 0.2, weight: 2, fillOpacity: 0.05 }
            });
            document.getElementById('Portland').bounds = boundaryLayer;
        });
        Paste this below the other similar statements and change all the instances of "portland" to the new town name.
        Make sure fetch('boundaries/townname.geojson') matches the exact name of the file you downloaded and renamed (case-sensitive)
        Also make sure that in document.getElementById('townname').bounds = boundaryLayer; the townname matches the internal id you made in step 1
        You should now have a town boundary that shows up when the town is selected.
    Now you should have a working town tab and town boundary.

If you have any additional questions, feel free to text me at 207-400-5997 (Cody LaBonty)

Bookmarks git fix
git restore .vscode/bookmarks.json