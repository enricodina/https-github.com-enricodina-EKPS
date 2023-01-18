<template>
    <div id="Airport-table">
        <table>
            <thead>
                <tr>
                    <th>AD name</th>
                    <th>AD ICAO</th>
                    <th>AD IATA</th>
                    <th>AD Lat</th>
                    <th>AD Long</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Dubai</td>
                    <td>OMDB</td>
                    <td>DXB</td>
                    <td>N25.00</td>
                    <td>E052.00</td>
                </tr>
                <tr>
                    <td>New Delhi</td>
                    <td>VIDP</td>
                    <td>DEL</td>
                    <td>N25.00</td>
                    <td>E062.00</td>
                </tr>
                <tr>
                    <td>Tehran</td>
                    <td>OIIE</td>
                    <td>IKA</td>
                    <td>N30.00</td>
                    <td>E052.00</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        name: "Airport-table"
    };
</script>

<style scoped>
</style>
