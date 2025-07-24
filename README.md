In this endpoint, my goal is to count how many unique bags have been scanned for each destination gate within the last N minutes.

So first, I extract the since_minutes query parameter — if the client doesn’t pass it, I default it to 60. I then calculate the cutoff timestamp using the current time minus that many minutes.

Next, I filter the BagScan table for all records that were scanned after that cutoff time. From those filtered results, I group the data by destination_gate, and use COUNT(DISTINCT bag_tag_id) to ensure each bag is counted only once per gate.

This way, even if the same bag was scanned multiple times at the same gate, it’s still counted only once — which gives a more accurate picture of how many different bags are active at each gate.

Finally, I return the results as a list of JSON objects, where each object has the destination_gate and the corresponding bag_count. It’s useful for operations dashboards or load distribution monitoring.”
