# Analysis

## 1. Highest Inefficiency Ratio

London had the highest inefficiency ratio at 2.42, followed by Frankfurt at 2.08. This was surprising because looking at the submarine cable map, there's a massive bundle of cables crossing the North Atlantic between the US East Coast and Western Europe. It's easily the densest cluster on the entire map, so the routing between Boston and London should be very direct.

The reason the ratio is so high is that London's theoretical minimum is only 52.6 ms, which is really small. So the fixed overhead from TCP handshakes, HTTP request/response processing, and routing through intermediate hops ends up being a big chunk of the total measured RTT. For farther cities like Tokyo or Mumbai, the theoretical minimum is already over 100 ms, so that same overhead barely affects the ratio.

## 2. Closest to Theoretical Minimum

Mumbai had the closest ratio above 1.0 at 1.05, meaning the measured RTT was only about 5% higher than the physical limit. Singapore (0.80) and Sydney (0.79) actually came in below 1.0, which shouldn't be possible since nothing can beat the speed of light through fiber. What's going on is that Google serves HTTP responses from nearby CDN servers, not from a server actually located in Singapore or Sydney. So when I hit google.com.sg, the response probably came from a Google data center somewhere in the US, which makes the measured RTT way lower than the real distance would suggest.

## 3. Lagos Routing Through Europe

Looking at the submarine cable map, the reason is pretty clear. The West African coast has cables running along it, but they all go north toward Europe. You can see them hugging the coast up through Senegal, Morocco, and landing in Portugal, Spain, France, and the UK. There is basically no cable going directly west from West Africa across the Atlantic to the US or South America. So a packet from Boston to Lagos almost certainly crosses the Atlantic to Europe first, then gets routed back south along the African coast to Nigeria.

You can also see on the map that compared to the North Atlantic (which has a huge dense bundle of cables between the US and Europe), the connections going down to West Africa are much thinner. Fewer cables means less capacity and fewer direct routing options.

To fix this you would need direct submarine cables between Africa and the Americas instead of always going through Europe. There are newer projects like the 2Africa cable that circles the whole continent, which should help. You'd also need more internet exchange points within Africa so that traffic between African countries can stay local instead of bouncing through European hubs for routing.
