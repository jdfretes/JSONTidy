<script lang="ts">
	import '../app.css';

	let jsonString: string = '';

	function formatJson() {
		try {
			const parsedJson = JSON.parse(jsonString);
			jsonString = JSON.stringify(parsedJson, null, 2);
		} catch (e) {
			alert('Invalid JSON');
		}
	}

	function highlightJson(jsonString: string) {
		const jsonHtml = jsonString
			.replace(/&/g, '&amp;')
			.replace(/</g, '&lt;')
			.replace(/>/g, '&gt;')
			.replace(
				/("(\\u[a-zA-Z0-9]{4}|\\[^u]|[^\\"])*"(\s*:)?|\b(true|false|null)\b|\b(-?\d+(?:\.\d*)?(?:[eE][+\-]?\d+)?)\b)/g,
				(match) => {
					if (/^"/.test(match)) {
						if (/:$/.test(match)) {
							// Claves JSON (strings seguidos por ':')
							return `<span class="text-lime-500">${match}</span>`;
						} else {
							// Valores de cadena JSON (strings sin ':')
							return `<span class="text-orange-500">${match}</span>`;
						}
					} else if (/true|false|null/.test(match)) {
						// Literales JSON: true, false, null
						return `<span class="text-indigo-500">${match}</span>`;
					} else {
						// Números JSON
						return `<span class="text-red-500">${match}</span>`;
					}
				}
			);
		return jsonHtml;
	}

	function copyJson() {
		navigator.clipboard.writeText(jsonString);
	}

	function handleFileChange(event: Event) {
		const input = event.target as HTMLInputElement;
		const file = input.files?.[0];
		if (file) {
			const reader = new FileReader();
			reader.onload = () => {
				const fileContent = reader.result as string;
				jsonString = fileContent;
				formatJson(); // Formatear el JSON cargado
			};
			reader.readAsText(file);
		}
	}

	function scrollToTop() {
		window.scrollTo({
			top: 0,
			behavior: 'smooth'
		});
	}
</script>

<nav>
	<div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
		<div class="relative flex h-16 items-center justify-between">
			<div class="flex flex-1 items-center justify-center sm:items-stretch sm:justify-start">
				<div class="flex space-x-4">
					<a
						href="/"
						class="rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white"
						aria-current="page"
					>
						{'{JSONTidy}'}
					</a>
				</div>
			</div>
		</div>
	</div>
</nav>

<form class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
	<div
		class="w-full mb-4 border border-gray-200 rounded-lg bg-gray-50 dark:bg-gray-700 dark:border-gray-600"
	>
		<div class="h-2/4 px-4 py-2 bg-white rounded-t-lg dark:bg-gray-800">
			<textarea
				id="json"
				bind:value={jsonString}
				rows="10"
				class="w-full px-0 text-sm text-gray-900 bg-white border-0 dark:bg-gray-800 focus:ring-0 dark:text-white dark:placeholder-gray-400"
				placeholder="Paste json here..."
				required
			></textarea>
		</div>

		<div class="flex items-center justify-between px-3 py-2 border-t dark:border-gray-600">
			<button
				on:click={formatJson}
				type="button"
				class="inline-flex items-center py-2.5 px-4 text-xs font-medium text-center text-white bg-red-700 rounded-lg focus:ring-4"
			>
				Format
			</button>
			<button
				on:click={copyJson}
				type="button"
				class="inline-flex items-center py-2.5 px-4 text-xs font-medium text-center text-white bg-green-700 rounded-lg focus:ring-4"
			>
				Copy
			</button>

			<div class="flex ps-0 space-x-1 rtl:space-x-reverse sm:ps-2">
				<input
					type="file"
					id="fileInput"
					on:change={handleFileChange}
					accept=".json"
					style="display: none;"
				/>

				<button
					type="button"
					on:click={() => {
						document.getElementById('fileInput')?.click();
					}}
					class="inline-flex justify-center items-center p-2 text-gray-500 rounded cursor-pointer hover:text-gray-900 hover:bg-gray-100 dark:text-gray-400 dark:hover:text-white dark:hover:bg-gray-600"
				>
					<svg
						class="w-4 h-4"
						aria-hidden="true"
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 12 20"
					>
						<path
							stroke="currentColor"
							stroke-linejoin="round"
							stroke-width="2"
							d="M1 6v8a5 5 0 1 0 10 0V4.5a3.5 3.5 0 1 0-7 0V13a2 2 0 0 0 4 0V6"
						/>
					</svg>
					<span class="sr-only">Attach file</span>
				</button>
			</div>
		</div>
		<code class="formatted-json">
			{@html highlightJson(jsonString)}
		</code>

		<button
			on:click={scrollToTop}
            style="right: 20%;"
			class="fixed bottom-4 bg-gray-900 text-white px-4 py-2 rounded-full shadow-md hover:bg-gray-800 focus:outline-none focus:ring-2 focus:ring-gray-600"
		>
			<svg
				xmlns="http://www.w3.org/2000/svg"
				class="h-6 w-6"
				fill="none"
				viewBox="0 0 24 24"
				stroke="currentColor"
			>
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 15l7-7 7 7" />
			</svg>
		</button>
	</div>
</form>

<p class="ms-auto text-xs text-gray-500 dark:text-gray-400 mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
	<a
		target="_blank"
		href="https://www.linkedin.com/in/juanfretes/"
		class="text-blue-600 dark:text-blue-500 hover:underline"
	>
		@juanfretes
	</a>
</p>

<style>
	.formatted-json {
		white-space: pre-wrap;
		word-break: break-all;
		color: white;
		font-size: 12px;
		font-family: monospace;
	}
</style>
