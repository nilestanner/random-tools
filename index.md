layout: default title: Main Project Directory

<div class="py-6">
<h1 class="text-4xl sm:text-5xl font-extrabold text-blue-700 mb-8 border-b-4 border-blue-100 pb-3">
Project Directory
</h1>

<p class="text-lg text-gray-600 mb-10">
    This is a dynamic index. It uses Jekyll's Liquid templating to automatically discover and list all top-level sub-projects that contain an HTML page.
</p>

<div class="space-y-6">
    {% comment %}
      1. Group all HTML pages by their directory path ('dir').
      2. This results in an array of directory names, which we iterate over.
    {% endcomment %}
    {% assign projects = site.html_pages | group_by: 'dir' %}

    {% for project in projects %}
        {% assign dir_path = project.name | remove: "/" %}

        {% comment %}
          Filter out the root directory ("") and Jekyll's internal folders
          like _site, _layouts, etc., to only list the project folders.
        {% endcomment %}
        {% if dir_path != "" and dir_path != "_site" and dir_path != "_layouts" and dir_path != "_includes" and dir_path != "_sass" and dir_path != "assets" %}

            <a href="/{{ dir_path }}/" class="block p-4 sm:p-6 bg-white border border-gray-200 rounded-xl shadow-lg transition duration-300 ease-in-out hover:shadow-xl hover:bg-blue-50">
                <h2 class="text-2xl font-semibold text-gray-900 flex items-center">
                    <!-- Folder Icon SVG -->
                    <svg class="w-7 h-7 mr-3 text-blue-500" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 7v10a2 2 0 002 2h14a2 2 0 002-2V9a2 2 0 00-2-2h-6l-2-2H5a2 2 0 00-2 2z"></path></svg>
                    
                    <!-- Format the directory name for display -->
                    {{ dir_path | replace: "-", " " | capitalize }}
                </h2>
                <p class="text-md text-gray-500 mt-2 ml-10">
                    Click here to view the <strong>{{ dir_path }}</strong> sub-project.
                </p>
            </a>

        {% endif %}
    {% endfor %}

    {% comment %} Fallback message if no projects are found {% endcomment %}
    {% if projects.size <= 1 %}
        <div class="p-6 bg-yellow-50 border-l-4 border-yellow-400 rounded-lg text-yellow-800">
            <p class="font-medium">No Sub-Projects Found</p>
            <p class="text-sm mt-1">Make sure your sub-directories contain at least one file recognized by Jekyll (e.g., an HTML file or a Markdown file).</p>
        </div>
    {% endif %}
</div>

<p class="mt-12 pt-6 border-t border-gray-200 text-sm text-center text-gray-400">
    Last Generated: {{ site.time | date: "%B %-d, %Y at %I:%M %p" }}
</p>


</div>