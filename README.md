
---

# 🎨 Advanced Paint Sequencer

A zero-installation, single-file web tool designed for model builders, hobbyists, and anyone performing sequential painting tasks. This application calculates the most efficient painting order to minimize the number of color changes and cleaning sessions, saving you time and effort.

The entire project state can be saved and shared via a single URL, making it easy to store your project plans or collaborate with others.



### [Try the Live Demo!](https://aasmith.github.io/paint-sequencer/painter.html)

## Key Features

*   **Interactive UI:** No more typing into a text box. Manage available paints and parts in dedicated lists.
*   **Visual Sequencer:** Assign, re-order, and remove paint steps for each part individually using a clean user interface.
*   **Optimal Schedule Generation:** The core logic analyzes all your part sequences and computes a step-by-step schedule that minimizes paint swaps.
*   **Completion Notices:** The generated schedule clearly indicates when a part has received its final coat of paint and is finished.
*   **Stateful Warnings:** The app warns you before you delete a paint or part that is currently in use, preventing mistakes. It also warns you about unused paints or unsequenced parts before generation.
*   **"Stamp" Tool for Bulk Actions:** Quickly apply a single paint color to multiple parts in specific positions without tedious clicking through dropdowns.
*   **Save & Share via URL:** Save your entire project—title, paints, parts, and sequences—into a compact URL hash. Copy the link to save it for later or share it with others. Loading the URL restores the project perfectly.
*   **Zero Dependencies:** The entire application is a single, self-contained HTML file. No installation, no servers, no setup needed. It runs entirely in your browser.

## How to Use

The workflow is designed to be simple and intuitive.

1.  **Set a Title:** Give your project a name at the top of the page.
2.  **Setup Paints and Parts:**
    *   In the "Available Paints" card, type the names of the colors you will be using. You can add them one at a time or enter a comma-separated list (e.g., `primer, red, metallic silver, clearcoat`) and click "Add".
    *   Do the same for the "Parts to be Painted" card (e.g., `fuselage, left wing, right wing, landing gear`).
3.  **Assign Paint Sequences:**
    *   For each part, use the dropdown menu on the right to select a paint and click "Add".
    *   Re-order steps using the `←` and `→` arrow buttons.
    *   Remove a step by clicking the `×` icon on the paint tag.
4.  **Bulk Assign with the Stamp Tool (Optional):**
    *   Click the **🖌️ Stamp Tool** button to enter stamp mode.
    *   Select the paint you want to apply from the "Stamping with:" dropdown in the toolbar that appears.
    *   The UI will change to show drop targets (`+`) at the beginning, end, and between every existing paint step for each part.
    *   Click any drop target to instantly insert the selected paint at that location.
    *   When finished, click **Finish Stamping**.
5.  **Generate the Schedule:**
    *   Click the **✨ Generate Optimal Order** button.
    *   If there are any issues (like parts without a sequence), the app will warn you before proceeding.
6.  **Review and Save:**
    *   Review your optimized schedule in the output card.
    *   Click the **💾 Save & Copy Link** button. This saves your current state to the URL and copies the link to your clipboard. You can now bookmark this link or share it. The "Save" button will turn green to indicate when you have unsaved changes.

## How the Optimization Works

The algorithm's goal is to minimize the number of times you have to load a new color into your airbrush or clean your paint brush. It does this using a greedy approach with an intelligent tie-breaker:

1.  It looks at all parts that still need painting.
2.  For each available paint, it counts how many parts are ready for that specific color as their *next* step.
3.  It finds the color that can be applied to the maximum number of parts.
4.  **Tie-Breaker:** If multiple colors could be applied to the same number of parts, it prioritizes the color that "unblocks" more future work. For example, painting a `primer` on three parts is considered more valuable than painting a final `clearcoat` on three parts, because the primer enables three new painting steps, while the clearcoat finishes them.
5.  It adds this chosen paint step to the schedule and repeats the process until all parts are complete.

## How to Run Locally

Since this is a self-contained application, you can run it without any special tools.
1.  Download the `painter.html` file.
2.  Open it in any modern web browser like Chrome, Firefox, Safari, or Edge.
