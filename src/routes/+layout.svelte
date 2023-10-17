<script>
	import '../app.postcss';
</script>

<!--
  Make sure you add some bottom padding to pages that include a sticky banner like this to prevent
  your content from being obscured when the user scrolls to the bottom of the page.
-->
<div
	class="pointer-events-none fixed inset-x-0 top-5 sm:flex sm:justify-center sm:px-6 sm:pb-5 lg:px-8"
>
	<div
		class="pointer-events-auto flex items-center justify-center gap-x-6 bg-gray-900 px-6 py-2.5 sm:rounded-xl sm:py-3 sm:pl-4 sm:pr-3.5"
	>
		<p class="text-sm leading-6 text-white">
			<strong class="font-semibold pr-1">BDA Project </strong>
		</p>
	</div>
</div>

<slot />
