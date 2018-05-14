1. Add a hub group contribution to your extension manifest:

    ```
    {
        "contributions": [
            {
                "id": "sample-hub-group",
                "type": "ms.vss-web.hub-group",
                "targets": [
                    "ms.vss-web.project-hub-groups-collection"
                ],
                "properties": {
                    "name": "Samples",
                    "order": 100
                }
            }
        ]
    }
    ```

	Look at the contribution targets reference to see the [available hub groups that can be contributed to](../../reference/targets/overview.md#targets).

2. Change your existing hub contribution to target the new hub group contribution:

    ```
    {
        "contributions": [
            {
                "id": "sample-hub",
                "type": "ms.vss-web.hub",
                "targets": [
                    ".sample-hub-group"
                ],
                "properties": {
                    "name": "Hello",
                    "order": 99,
                    "uri": "hello-world.html"
                }
            }
        ]
    }
    ```

4. [Install](../../develop/install.md) your extension.

   Now your hub appears under your Samples hub group.

   ![Hello hub in the Samples hub group](./_img/create-hub-group/hub-group.png)
