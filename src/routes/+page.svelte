<script>
	import '../app.css';
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
                        >{'{JSONTidy}'}
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
        <div class="h-2/4 px-4 py-2 bg-white rounded-t-lg dark:bg-gray-800 ">
            <textarea
                id="comment"
                rows="30"
                class="w-full px-0 text-sm text-gray-900 bg-white border-0 dark:bg-gray-800 focus:ring-0 dark:text-white dark:placeholder-gray-400"
                placeholder="Paste json here..."
                required
            ></textarea>
        </div>
        <div class="flex items-center justify-between px-3 py-2 border-t dark:border-gray-600">
            <button
                type="submit"
                class="inline-flex items-center py-2.5 px-4 text-xs font-medium text-center text-white bg-blue-700 rounded-lg focus:ring-4 focus:ring-blue-200 dark:focus:ring-blue-900 hover:bg-blue-800"
            >
                Format
            </button>
            <div class="flex ps-0 space-x-1 rtl:space-x-reverse sm:ps-2">
                <button
                    type="button"
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
    </div>
</form>
<p
    class="ms-auto text-xs text-gray-500 dark:text-gray-400 mx-auto max-w-7xl px-2 sm:px-6 lg:px-8"
>
    <a
        target="_blank"
        href="https://www.linkedin.com/in/juanfretes/"
        class="text-blue-600 dark:text-blue-500 hover:underline">@juanfretes</a
    >
</p>