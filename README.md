
# News Frontend

Fron-end uses Vue

There are two components dedicated for News. App imports NewsList. NewsList fetches news list from backend instead of App because I believe NewsList is the only component that requires news and App could be used as the root for many future components. NewsList contains News components which are individual list items. List items can be expanded upon click. Expansion includes content, title, url, author, source, and date. They also contain save button and collapse button. Save button communicates with backend and collapse button collapses expasion.
