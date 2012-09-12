Routes
======

Fetch a single route
--------------------

**GET /route/id/**

Response

::

    {
        "distance_in_meters": "9972.24",
        "id": 149,
        "is_favorite": true,
        "name": "6.2 mi in Danville, CA",
        "resource_uri": "/api/v1/route/149/",
        "source": "Athlete.com iPhone App",
        "static_map_url": "http://maps.googleapis.com/maps/api/staticmap?path=color:0xe74d2acc|weight:3|enc:cb%7BeFdiugV%7EA%7BBdAcD%60BqCxAwC%7C%40yC%7CAsC%7CAiCzAkCtAyC%7EAsCtA_DhBqCzA%7DC%7CAyCrBu%40%60BgClA%7BCxEgH%7E%40mCiBhCaBlC%7D%40zDwBtBaB%7CC%7BBpAsA%60DeChDiDlIiDtE_A%60DeBlC%7BFvLaB%7CCcBnCkBpC%7DAnDyBbC%7DCxCqEdG_C%60BaBrC%7DBrAmAxCiB%60CiJdJyBbB%7DCfGoG%7EEuBnCaCtBiBlCkClA%7BGxEqCn%40gCbBaCrBiB%60CyBlByBfCcCvAqEzFaClBeBbCyHtLmBzBmBnCyAlDqBvBoBhC%7BAbDcCbBkCvAsCt%40gD%5E%5Ec%40nDe%40%7EFeBxBgCpBsBzBoCbB_DrBkCjCkBjAiDdByC%7ECgEpB_C%7CBsBlBkBvEsG%7CBuBpBsBvBcC%7EB_BdCcAbCyA%7CBmBhC%7DAlA%7B%40&sensor=false&maptype=roadmap&key=AIzaSyC4dBdwntTxOB-ookwMn74n3qS9lSF3ccc"
    }


Toggle the favorited status of this route for the current user
--------------------------------------------------------------

**POST /route/id/toggle_favorite/**

Response will contain the favorite stats after the toggle.

::

    { "is_favorite": true }
