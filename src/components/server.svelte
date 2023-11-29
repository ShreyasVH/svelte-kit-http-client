<script>
    import { onMount } from 'svelte';
    import { get, post, put, del } from '../utils/api'

    let data = {
        get: '',
        post: '',
        put: '',
        delete: ''
    };

    export let endpoint;

    let urls = {
        get: endpoint + '/api?input=abc',
        post: endpoint + '/api',
        put: endpoint + '/api',
        delete: endpoint + '/api?input=abc'
    };

    const payload = {
        a: 'A',
        b: 'B'
    };

    onMount(async () => {
        const getResponse = await get(urls.get);
        const postResponse = await post(urls.post, payload);
        const putResponse = await put(urls.put, payload);
        const deleteResponse = await del(urls.delete);

        data = {
            get: JSON.stringify(getResponse.data),
            post: JSON.stringify(postResponse.data),
            put: JSON.stringify(putResponse.data),
            delete: JSON.stringify(deleteResponse.data)
        };
    });

</script>

<div>
    <div>
        <div>
            {#each Object.keys(urls) as type}
            <div>
                <p>
                    <b>
                        URL:
                    </b>
                    &nbsp;
                    <span>
                        {urls[type]}
                    </span>
                </p>

                <p>
                    <b>
                        Response:
                    </b>
                    &nbsp;
                    <span>
                      {data[type]}
                  </span>
                </p>
            </div>
            {/each}
        </div>
    </div>
</div>

