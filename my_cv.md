# <font face="'Consolas', 'Menlo', 'Courier New'" color=#2f9e44>**My CV**</font>

<font face="'Consolas', 'Menlo', 'Courier New'" color=#2f9e44>Thanks for your interest! This is my CV</font> 🫡

<embed src="kf-cv.pdf" type="application/pdf" width="100%" height="600px" />

<div style="text-align: center;">
    <font face="'Consolas', 'Menlo', 'Courier New'" color=#2f9e44 id="lastUpdated"></font>
</div>
<script>
    // Set the last updated date
    document.addEventListener('DOMContentLoaded', function() {
        var metaTag = document.querySelector('meta[name="docbuild:last-update"]');
        if (metaTag) {
            var buildDate = metaTag.getAttribute('content');
            var lastUpdatedElement = document.getElementById('lastUpdated');
            lastUpdatedElement.textContent = 'Last updated: ' + buildDate;
        }
    });
</script>