---
layout: default
---

<a href="index.html#talks" class="back-link">
    <i data-feather="arrow-left"></i>
    Back to Talks
</a>

<div class="poster-header">
    <h1>Quantum Transistor in Superconducting Circuits</h1>
    <p>SIFISC Conference - September 2021</p>
</div>

<div class="poster-viewer">
    <div class="poster-controls">
        <h2 class="poster-title">Poster Viewer</h2>
        <div class="control-buttons">
            <button class="control-btn" onclick="prevPage()" id="prevBtn">
                <i data-feather="chevron-left"></i>
                Previous
            </button>
            <span class="page-info" id="pageInfo">Loading...</span>
            <button class="control-btn" onclick="nextPage()" id="nextBtn">
                Next
                <i data-feather="chevron-right"></i>
            </button>
            <button class="control-btn" onclick="downloadPDF()">
                <i data-feather="download"></i>
                Download
            </button>
        </div>
    </div>

<div class="poster-content">
    <div class="loading-message" id="loadingMessage">
        <div class="loading-spinner"></div>
        <p>Loading poster...</p>
    </div>
    <canvas id="pdfCanvas" style="display: none;"></canvas>
    <div class="error-message" id="errorMessage" style="display: none;">
        <strong>Error loading PDF:</strong>
        <p>Could not load the poster.pdf file. Please verify that the file exists in the correct directory.</p>
    </div>
</div>

</div>
<script>
        let pdfDoc = null;
        let pageNum = 1;
        let pageRendering = false;
        let pageNumPending = null;
        const scale = 1.5;
        const canvas = document.getElementById('pdfCanvas');
        const ctx = canvas.getContext('2d');
        const pdfUrl = '/assets/building_block.pdf';

        function renderPage(num) {
            pageRendering = true;
            pdfDoc.getPage(num).then(function(page) {
                const viewport = page.getViewport({scale: scale});
                canvas.height = viewport.height;
                canvas.width = viewport.width;

                const renderContext = {
                    canvasContext: ctx,
                    viewport: viewport
                };

                const renderTask = page.render(renderContext);
                renderTask.promise.then(function() {
                    pageRendering = false;
                    if (pageNumPending !== null) {
                        renderPage(pageNumPending);
                        pageNumPending = null;
                    }
                    updatePageInfo();
                });
            });
        }

        function queueRenderPage(num) {
            if (pageRendering) {
                pageNumPending = num;
            } else {
                renderPage(num);
            }
        }

        function updatePageInfo() {
            document.getElementById('pageInfo').textContent = `Page ${pageNum} of ${pdfDoc.numPages}`;

            // Update button states
            document.getElementById('prevBtn').disabled = pageNum <= 1;
            document.getElementById('nextBtn').disabled = pageNum >= pdfDoc.numPages;
        }

        function prevPage() {
            if (pageNum <= 1) return;
            pageNum--;
            queueRenderPage(pageNum);
        }

        function nextPage() {
            if (pageNum >= pdfDoc.numPages) return;
            pageNum++;
            queueRenderPage(pageNum);
        }

        function downloadPDF() {
            const link = document.createElement('a');
            link.href = pdfUrl;
            link.download = './poster.pdf';
            link.click();
        }

        function toggleMenu() {
            document.getElementById('navLinks').classList.toggle('open');
        }

        // Initialize PDF viewer
        document.addEventListener('DOMContentLoaded', function() {
            feather.replace();

            pdfjsLib.getDocument(pdfUrl).promise.then(function(pdf) {
                pdfDoc = pdf;
                document.getElementById('loadingMessage').style.display = 'none';
                document.getElementById('pdfCanvas').style.display = 'block';
                renderPage(pageNum);
            }).catch(function(error) {
                console.error('Error loading PDF:', error);
                document.getElementById('loadingMessage').style.display = 'none';
                document.getElementById('errorMessage').style.display = 'block';
            });
        });

        // Keyboard navigation
        document.addEventListener('keydown', function(e) {
            if (e.key === 'ArrowLeft') {
                prevPage();
            } else if (e.key === 'ArrowRight') {
                nextPage();
            }
        });

</script>
