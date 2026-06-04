try {

const host = window.location.hostname.toLowerCase();
if (!host.includes("emaint.com")) {
  alert(`X4 - Tools is restricted to emaint.com sites.\n\nCurrent site:\n${host}`);
  return;
}

const baseUrl = `${location.protocol}//${location.host}/`;

const X4 = {};

let dragMoveRef = null;
let dragUpRef = null;

X4.close = function () {
  document.getElementById("x4-root")?.remove();

  document.removeEventListener("keydown", X4.escHandler);

  if (dragMoveRef) {
    document.removeEventListener("mousemove", dragMoveRef);
    dragMoveRef = null;
  }

  if (dragUpRef) {
    document.removeEventListener("mouseup", dragUpRef);
    dragUpRef = null;
  }
};

X4.escHandler = (e) => {
  if (e.key === "Escape") X4.close();
};

X4.open = function (path) {
  const url = baseUrl + path;
  window.open(url) || (location.href = url);
  X4.close();
};

X4.toggle = function (id) {
  const section = document.getElementById(id);
	if (!section) return;

  const title = section.previousElementSibling;
	if (!title) return;

  const isOpen = getComputedStyle(section).display !== "none";
  section.style.display = isOpen ? "none" : "flex";

  const arrow = title.querySelector("span");
  if (arrow) arrow.style.transform = isOpen ? "rotate(0deg)" : "rotate(90deg)";
};

window.X4 = X4;

/* ================= CONFIG Menu ================= */

const menuConfig = [
  {
    title: "Main Menu",
    items: [
      { label: "User Administration", url: "wc.dll?X3~emproc~x3Hubv2#/USERRIGHTS" },
      { label: "Account Settings", url: "wc.dll?X3~emproc~x3Hubv2~accountsettings" },
      { label: "Manage Deleted Records", url: "wc.dll?X3~emproc~x3Hubv2#/__/WDNIVUIubG9hZE1hbmFnZURlbGV0ZWRSZWNvcmRzR28oKQ==" },
      { label: "Meter Manager", url: "wc.dll?X3~emproc~x3Hubv2#/shortcut/d2MuZGxsP3gzfmVtcHJvY35tZXRlcm1hbmFnZXI="  },
      { label: "X3 Menu", url: "wc.dll?x3~emproc~uiMenu~&gotab=x3Menu" }
    ]
  },

  {
    title: "User Tables",
    searchable: true,
    items: [
      { label: "Charges", url: "wc.dll?X3~emproc~x3Hubv2#/charges" },
      { label: "Reports", url: "wc.dll?X3~emproc~x3Hubv2#/X4REPORTS" },
      { label: "Contacts", url: "wc.dll?x3~emproc~x3hubv2#/CONTACT" },
      { label: "Assets", url: "wc.dll?x3~emproc~x3hubv2#/COMPINFO" },
      { label: "Tasks", url: "wc.dll?X3~emproc~x3Hubv2#/Tasks" },
      { label: "Task Procedures", url: "wc.dll?X3~emproc~x3Hubv2#/TASK_PROCS" },
      { label: "Workflow", url: "wc.dll?X3~emproc~x3Hubv2#/WORKFLOW" },
      { label: "WF Email Template", url: "wc.dll?X3~emproc~filelist~&ACTION=LIST&KEYFIELD=CUID&TABLE=WFEMAIL&MESSAGE=&WIND=0" },
      { label: "Projects", url: "wc.dll?X3~emproc~x3Hubv2#/PROJECT" },
      { label: "WO Assignments", url: "wc.dll?X3~emproc~x3Hubv2#/WOASSIGN" },
      { label: "WO Sign-On Tracking", url: "wc.dll?X3~emproc~x3Hubv2#/WOSIGNON" },
      { label: "User Clock-In Tracking", url: "wc.dll?X3~emproc~x3Hubv2#/USERCLOCK" },
      { label: "WO Procedures", url: "wc.dll?X3~emproc~x3Hubv2#/WO_PROCS" },
      { label: "WO Documents", url: "wc.dll?X3~emproc~x3Hubv2#/WO_DOCS" },
      { label: "WO Parts Requirements", url: "wc.dll?X3~emproc~x3Hubv2#/WOPARTSRQD" },
      { label: "Work Permit", url: "wc.dll?X3~emproc~x3Hubv2#/WORKPERMIT" },
      { label: "Scheduled Activity", url: "wc.dll?X3~emproc~x3Hubv2#/PM" },
      { label: "PM Assignments", url: "wc.dll?X3~emproc~x3Hubv2#/PMASSIGN" },
      { label: "PM Procedures", url: "wc.dll?X3~emproc~x3Hubv2#/PM_PROCS" },
      { label: "PM Documents", url: "wc.dll?X3~emproc~x3Hubv2#/PM_DOCS" },
      { label: "Purchase Orders", url: "wc.dll?x3~emproc~x3hubv2#/POMAST" },
      { label: "PO Transaction", url: "wc.dll?X3~emproc~x3Hubv2#/POTRAN" },
      { label: "Pending Requisition Approvals", url: "wc.dll?X3~emproc~x3Hubv2#/RQAPRV" },
      { label: "Approval Groups", url: "wc.dll?X3~emproc~x3Hubv2#/RQDEPT" },
      { label: "Inventory Journal", url: "wc.dll?X3~emproc~x3Hubv2#/ICJOURNL" },
      { label: "Parts Location", url: "wc.dll?x3~emproc~x3Hubv2#/INVLOC" },
      { label: "Items By Supplier", url: "wc.dll?X3~emproc~x3Hubv2#/INVSUPL" },
      { label: "Meter Readings", url: "wc.dll?X3~emproc~x3Hubv2#/METER" },
      { label: "Monitor Points Readings", url: "wc.dll?X3~emproc~x3Hubv2#/MON_READ" },
      { label: "Asset Parts Cross Reference", url: "wc.dll?X3~emproc~x3Hubv2#/COMPPART" },
      { label: "Doc. Storage", url: "wc.dll?x3~emproc~x3Hubv2~documentstorage" },
      { label: "Change Log", url: "wc.dll?X3~emproc~x3Hubv2#/CHANGESLOG" }
    ]
  },

  {
    title: "Support Tables",
    items: [
      { label: "Data Dictionary", url: "wc.dll?X3~emproc~x3Hubv2#/DATADICT" },
      { label: "User Preference", url: "wc.dll?X3~emproc~x3Hubv2#/USERPREF" },
      { label: "Form Link", url: "wc.dll?X3~emproc~x3Hubv2#/FORMLINK" },
      { label: "WF Action Table", url: "wc.dll?X3~emproc~filelist~&ACTION=LIST&TABLE=WFACTION&KEYFIELD=CFLOWID" },
      { label: "Forms List", url: "wc.dll?x3~emproc~x3Hubv2#/DDFRMLIST" },
	  { label: "Extra Field Mapping", url: "wc.dll?x3~emproc~filelist~&ACTION=LIST&TABLE=lookups&KEYFIELD=cluname" },
      { label: "RT EXTRA", url: "wc.dll?X3~emproc~x3Hubv2#/RTEXTRA" },
      { label: "Forms Dictionary", url: "wc.dll?X3~emproc~x3Hubv2#/DDFORMS" },
      { label: "Q.T. Master File (Filters - X3 View)", url: "wc.dll?x3~emproc~filelist~&ACTION=LIST&TABLE=QTMASTER&KEYFIELD=CUID" },
      { label: "Q.T. Calculated Fields", url: "wc.dll?X3~emproc~x3Hubv2#/QTCALCFLDS" }
    ]
  },

  {
    title: "Database Tools",
    items: [
      { label: "Reindex", url: "wc.dll?X3~emproc~reindex", highlight: true },
      { label: "Verstrus", url: "wc.dll?X3~emproc~verstrus", highlight: true },
      { label: "Data Import / Delete", url: "wc.dll?X3~emproc~importdata~&support=on" },
      { label: "Mass Key Change", url: "wc.dll?X3~emproc~modcall~&MOD=X3KEYCHANGE&METH=MODLOAD&PR=1" },
      { label: "Health Check", url: "health_check.wc" }
    ]
  }
];

/* ================= RENDER ================= */

function buildMenu(config) {
  let html = "";

  config.forEach((section, i) => {
    const id = "sec_" + i;

    html += `
      <div class="x4section-title" data-toggle="${id}">
        ${section.title}
        <span>▶</span>
      </div>
      <div id="${id}" class="x4section">
    `;

    section.items.forEach(item => {
      const cls = item.highlight ? "danger" : "";
      html += `
        <button class="${cls}" data-url="${item.url}" data-label="${item.label}">
          ${item.label}
        </button>
      `;
    });

    html += `</div>`;
  });

  return html;
}

/* ================= UI ================= */

const X4Menu = (() => {

  let root = null;

  function mount() {

	document.getElementById("x4-root")?.remove();

	root = document.createElement("div");
	root.id = "x4-root";

    root.innerHTML = `
      <style>
        #x4menu {
			position: fixed;
			top: 6%;
			left: calc(50% - 160px);
			width: 290px;
			max-width: 90vw;
			height: auto;
			max-height: 90vh;

			display: flex;
			flex-direction: column;
			padding: 5px 10px;
			padding-bottom: 10px;

			z-index: 999999;

			background: rgba(17, 24, 39, 0.55);
			color: #f8fafc;

			border: 1px solid #374151;
			border-radius: 10px;
			backdrop-filter: blur(10px);

			box-shadow: 0 8px 24px rgba(0,0,0,.4);
			font-family: Arial, sans-serif;
			font-size: 13px;

			opacity: 0;                 /* start hidden */
			animation: popupFade 0.35s ease-out forwards; /* trigger animation */
		}

			/* Keyframes for fade + scale */
			@keyframes popupFade {
			  from {
				opacity: 0;
				scale(0.95);
			  }
			  to {
				opacity: 1;
				scale(1);
			  }
		}

		#x4header {
			font-weight: bold;
			margin-bottom: 6px;
			cursor: move;
			user-select: none;
			padding-right: 18px;
			font-size: 14px;           /* header slightly larger for hierarchy */
			color: #ffffff;
		}
		
		#x4body {
			flex: unset;
			max-height: 70vh;
			overflow-y: auto;
			overflow-x: hidden;	
			padding-right: 2px;
		}

		#x4closeX {
			position:absolute;
			top:5px;
			right:7px;
			width:20px;
			height:20px;
			display:flex;
			align-items:center;
			justify-content:center;
			cursor:pointer;
			border-radius:4px;
			transition:.15s;
		}
		
		#x4closeX:hover {
			background:rgba(255,255,255,.15);
		}

        #x4search {
          width: 100%;	

		  padding: 5px 10px;

		  margin-bottom: 8px;

		  border: 1px solid #4b5563;
		  border-radius: 6px;

		  background: rgba(17,24,39,0.6);
		  color: #f8fafc;

		  box-sizing: border-box;
		  font-size: 12px;
		}

		#x4search:focus {
		  outline: none;
		  border-color: #f43f5e; /* coral red accent */
		  box-shadow: 0 0 6px #f43f5e;
		}

        .x4section-title {
          display: flex;
		  justify-content: space-between;
		  align-items: center;

		  margin: 8px 0 4px;
		  padding: 5px 10px;

		  margin-top: 2px;

		  background: #111827;
		  border:1px solid #2d3748;
		  border-left:4px solid #dc2626;

		  border-radius: 6px;
		  color: #e5e7eb;
		  font-size: 13px;
		  font-weight: 600;
		  text-transform: uppercase;
		  letter-spacing:.7px;

		  transition:all .15s ease;
		  cursor: pointer;  		  
		}

		.x4section-title:hover {
		  background: #172033;
		  border-left-color:#ef4444;
		}

		.x4section-title span {
		  transition: transform .15s ease;
		}

        .x4section {
          display: none;
          padding: 6px;
          flex-direction: column;
          gap: 1px;
        }

		/* Sub-buttons inside sections */
        #x4menu button {
		    width: 100%;

			padding: 5px 10px;
			min-height: 30px;
			margin-top: 1px;

			border: 1px solid #4b5563;
			border-radius: 6px;
			transition: background .2s ease, border-color .2s ease, color .2s ease;

			background: rgba(31, 41, 55, 0.6); /* darker frosted gray */
			color: #ffffff;

			font-size: 12px;

			cursor: pointer;
			text-align: left;

			transition: .15s;

			white-space: normal;
			word-break: break-word;
		}

		#x4body::-webkit-scrollbar {
			width: 8px;
		}

		#x4body::-webkit-scrollbar-track {
			background: #111827;
		}

		#x4body::-webkit-scrollbar-thumb {
			background: linear-gradient(180deg, #f43f5e, #dc2626);
			border-radius: 8px;
		}

		#x4body::-webkit-scrollbar-thumb:hover {
			background: linear-gradient(180deg, #fb7185, #f43f5e);
		}

		/* Sub-button hover: */
		#x4menu button:hover {
			background: #dc2626;       
			border-color: #dc2626;
			color: #ffffff;
		}

        #x4menu button.danger {
			background: linear-gradient(135deg, rgba(220,38,38,.18), rgba(185,28,28,.10));
			border: 1px solid #dc2626;
			color: #fef2f2;
			font-weight: 700;
			
			padding: 5px 10px;
			box-shadow: 
				inset 0 0 6px rgba(220,38,38,.12),
				0 0 8px rgba(220,38,38,.12);
		}

		#x4menu button.danger:hover {
			background: #f59e0b;
			border-color: 1px solid #dc2626;
			color: #fef2f2;
			box-shadow: 0 0 12px rgba(245,158,11,.40);
		}
		
		.x4-selected {
			outline: 2px solid #dc2626;
			background: rgba(96,165,250,.15);
		}

        mark {
          background: #ffb3b3;
          font-weight: bold;
        }
      </style>

      <div id="x4menu">
        <div id="x4closeX">✕</div>
        <div id="x4header">X4 Tools</div>
        <input id="x4search" placeholder="Search..." />
        <div id="x4body">${buildMenu(menuConfig)}</div>
      </div>
    `;

    (document.body || document.documentElement).appendChild(root);

    bind();
    autoOpen();
    drag();
    searchInit();
  }

  function bind() {
  document.getElementById("x4body").addEventListener("click", (e) => {

    const btn = e.target.closest("button[data-url]");
    if (btn) return X4.open(btn.dataset.url);

    const toggle = e.target.closest("[data-toggle]");
    if (toggle) return X4.toggle(toggle.dataset.toggle);

  });

	const closeBtn = document.getElementById("x4closeX");

	if (closeBtn) {
	  closeBtn.addEventListener("click", X4.close);
	}

  document.removeEventListener("keydown", X4.escHandler);
  document.addEventListener("keydown", X4.escHandler);
}

  function autoOpen() {

  ["sec_2", "sec_3"].forEach(id => {

    const section = document.getElementById(id);
    if (!section) return;

    section.style.display = "flex";

    const arrow =
      section.previousElementSibling?.querySelector("span");

    if (arrow) {
      arrow.style.transform = "rotate(90deg)";
    }
  });
}

  function drag() {
    const box = document.getElementById("x4menu");
    const header = document.getElementById("x4header");
    if (!box || !header) return;

    let sx = 0, sy = 0, bx = 0, by = 0;
    let dragging = false;

    header.addEventListener("mousedown", (e) => {
      dragging = true;

      const r = box.getBoundingClientRect();
		box.style.left = r.left + "px";
		box.style.top = r.top + "px";
		box.style.transform = "none";

		sx = e.clientX;
		sy = e.clientY;
		bx = r.left;
		by = r.top;

      dragMoveRef = (e) => {
		if (!dragging) return;

			const newLeft = bx + (e.clientX - sx);
			const newTop = by + (e.clientY - sy);

			const maxLeft = window.innerWidth - box.offsetWidth;
			const maxTop = window.innerHeight - box.offsetHeight;

			box.style.left =
			Math.max(0, Math.min(newLeft, maxLeft)) + "px";
	 
			box.style.top =
			Math.max(0, Math.min(newTop, maxTop)) + "px";
		};

      dragUpRef = () => {
			dragging = false;

			document.removeEventListener("mousemove", dragMoveRef);
			document.removeEventListener("mouseup", dragUpRef);

			dragMoveRef = null;
			dragUpRef = null;
		};

		document.addEventListener("mousemove", dragMoveRef);
		document.addEventListener("mouseup", dragUpRef);

      e.preventDefault();
    });
}

    function searchInit() {
		const search = document.getElementById("x4search");
		if (!search) return;

		const idx = menuConfig.findIndex(s => s.title === "User Tables");
		const sec = document.getElementById("sec_" + idx);
		if (!sec) return;

		const buttons = sec.querySelectorAll("button");
		buttons.forEach(b => b.dataset.original = b.dataset.label);

		let selectedIndex = -1;

		search.addEventListener("input", () => {
			const value = search.value.toLowerCase();

			selectedIndex = -1;

			buttons.forEach(btn => {
				const original = btn.dataset.original;

				if (!value) {
					btn.style.display = "";
					btn.innerHTML = original;
					return;
				}

				const match = original.toLowerCase().includes(value);

				btn.style.display = match ? "" : "none";

				btn.innerHTML = match
				? highlight(original, search.value)
				: original;
			});

			if (value) {
				sec.style.display = "flex";

				const arrow =
				sec.previousElementSibling?.querySelector("span");

				if (arrow) {
					arrow.style.transform = "rotate(90deg)";
				}
			}
		});

		
		search.addEventListener("keydown", (e) => {
			const visibleButtons = [...buttons].filter(
				btn => btn.style.display !== "none"
			);

			if (!visibleButtons.length) return;

			if (e.key === "ArrowDown") {
				e.preventDefault();

				selectedIndex++;

				if (selectedIndex >= visibleButtons.length) {
					selectedIndex = 0;
				}

				updateSelection(visibleButtons);
			}

			if (e.key === "ArrowUp") {
				e.preventDefault();

				selectedIndex--;

				if (selectedIndex < 0) {
					selectedIndex = visibleButtons.length - 1;
				}

				updateSelection(visibleButtons);
			}

			if (e.key === "Enter") {
				e.preventDefault();

				const active = visibleButtons[selectedIndex];

				if (active) {
					active.click();
				}
			}
		});

		function updateSelection(visibleButtons) {
			visibleButtons.forEach(btn => {
			btn.classList.remove("x4-selected");
		});

		const active = visibleButtons[selectedIndex];

		if (!active) return;

			active.classList.add("x4-selected");

			active.scrollIntoView({
				block: "nearest"
			});
		}
	}
	
  function highlight(text, query) {
    const safe = query.replace(
      /[.*+?^${}()|[\]\\]/g,
      "\\$&"
    );

    return query
      ? text.replace(
          new RegExp(`(${safe})`, "gi"),
          "<mark>$1</mark>"
        )
      : text;
  }

  return { mount };
})();

/* ================= BOOT ================= */

document.getElementById("x4-root")?.remove();
X4Menu.mount();

} catch (err) {
  alert("X4 failed:\n" + err.message);
}
