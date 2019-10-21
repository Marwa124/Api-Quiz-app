<template>
    <div class="app-header">
        <b-nav tabs>
            <b-nav-item disabled=""><b>Quiz app</b></b-nav-item>
            <b-nav-item disabled="">{{numTotal}} / 10</b-nav-item>
        </b-nav>
    </div>
</template>

<script>
export default {
    props: [
        'numCorrect',
        'numTotal'
    ]
}
</script>
