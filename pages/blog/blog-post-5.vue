<template lang="md">
# Hello World!

Current route is: {{ $route.path }}

*Italic*, **bold**, and 'monospace'

    ```js
    <script>
        const foo = 'bar';
        console.log(foo);
    </script>
    ```

    Itemized lists look like:

        * this one
        * that one
        * the other one

> Block quotes are
> written like so.
</template>

<script>
export default {
    layout: 'blog'
}
</script>
