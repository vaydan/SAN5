// ==UserScript==
// @name        SAN5 | Slam and Sortable Info
// @namespace   Nik Vayda
// @version     3.1
// @description Shows slam, Sort Slam, Sort HCap, NC Slam, NC HCap, and XD Slam data for SAN5
// @author      vaydan
// @match       https://atrops-web-na.amazon.com/*
// @grant       none
// ==/UserScript==

(function() {
    'use strict';
    // Add auto-refresh functionality
    const refreshInterval = 120000; // 2 minutes in milliseconds

    function refreshPage() {
        location.reload();
    }

    setInterval(refreshPage, refreshInterval);

    function extractSortSlam() {
        const sortSlamElement = document.evaluate('/html/body/div[3]/div[8]/div[3]/table/tbody/tr[27]/td[20]/a', document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null);
        if (sortSlamElement.singleNodeValue) {
            const number = sortSlamElement.singleNodeValue.textContent.trim();
            return number;
        }
        return 'N/A';
    }

    function extractSortableCap() {
        const sortableCapElement = document.evaluate('/html/body/div[3]/div[8]/div[3]/table/tbody/tr[27]/td[18]', document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null);
        if (sortableCapElement.singleNodeValue) {
            const number = sortableCapElement.singleNodeValue.textContent.trim();
            return number;
        }
        return 'N/A';
    }

    function extractNCSlam() {
        const ncSlamElement = document.evaluate('/html/body/div[3]/div[8]/div[3]/table/tbody/tr[29]/td[20]/a', document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null);
        if (ncSlamElement.singleNodeValue) {
            const number = ncSlamElement.singleNodeValue.textContent.trim();
            return number;
        }
        return 'N/A';
    }

    function extractNCCap() {
        const ncCapElement = document.evaluate('/html/body/div[3]/div[8]/div[3]/table/tbody/tr[29]/td[18]', document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null);
        if (ncCapElement.singleNodeValue) {
            const number = ncCapElement.singleNodeValue.textContent.trim();
            return number;
        }
        return 'N/A';
    }

    function extractXDSlam() {
        const xdSlamElement = document.evaluate('/html/body/div[3]/div[8]/div[3]/table/tbody/tr[41]/td[20]/a', document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null);
        if (xdSlamElement.singleNodeValue) {
            const number = xdSlamElement.singleNodeValue.textContent.trim();
            return number;
        }
        return 'N/A';
    }

    function createDisplayBox() {
        const displayBox = document.createElement('div');
        displayBox.innerHTML = `
            <div style="position: fixed; top: 20px; right: 20px; z-index: 9999; font-size: 16px;">
                <div style="display: flex; align-items: center; background-color: white; padding: 15px; border: 2px solid black; text-align: center; color: black; line-height: 1.5em;">
                    <div style="max-width: 150px; margin-right: 10px;">
                        <img src="https://media.discordapp.net/attachments/1177112200515702854/1187123462096031814/IMG_2731.png?ex=6595bde1&is=658348e1&hm=36d65ff31fb21f4f7e2bb6eb82e2b966248a2c289f9fe6f17efe84262ddb21c7" alt="SAN5 Image" style="width: 150px; height: auto;">
                    </div>
                    <div style="font-size: 18px;">
                        <div style="font-weight: bold;">SAN5</div>
                        <div style="margin-bottom: 5px;">Sort Slam: <span id="sortSlam"></span></div>
                        <div style="margin-bottom: 5px;">Sort <i>HCap</i>: <span id="sortableCap"></span></div>
                        <div style="margin-bottom: 5px;">NC Slam: <span id="ncSlam"></span></div>
                        <div style="margin-bottom: 5px;">NC <i>HCap</i>: <span id="ncCap"></span></div>
                        <div style="margin-bottom: 5px;">XD Slam: <span id="xdSlam"></span></div>
                    </div>
                </div>
            </div>
        `;
        document.body.appendChild(displayBox);

        function updateSortSlam() {
            const sortSlamData = extractSortSlam();
            document.getElementById('sortSlam').innerText = sortSlamData;
        }

        function updateSortableCap() {
            const sortableCapData = extractSortableCap();
            document.getElementById('sortableCap').innerText = sortableCapData;
        }

        function updateNCSlam() {
            const ncSlamData = extractNCSlam();
            document.getElementById('ncSlam').innerText = ncSlamData;
        }

        function updateNCCap() {
            const ncCapData = extractNCCap();
            document.getElementById('ncCap').innerText = ncCapData;
        }

        function updateXDSlam() {
            const xdSlamData = extractXDSlam();
            document.getElementById('xdSlam').innerText = xdSlamData;
        }

        updateSortSlam();
        updateSortableCap();
        updateNCSlam();
        updateNCCap();
        updateXDSlam();
    }

    // Create the box when the page loads
    createDisplayBox();
})();
