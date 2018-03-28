---
#title How to test mainnet blockchain in an isolated test environment

---

<h1 id="how-to-test-mainnet-blockchain-in-an-isolated-test-environment">How to test mainnet blockchain in an isolated test environment</h1>
<p>So some core updates have been made to the blockchain project, they have been tested on separate testnets and all looks good. The changes are rather game changing and it would be great to test the mainnet blockchain just to be sure, as failing on mainnet means all kinds of trouble. The last thing anyone wants is a failed upgrade and a non-functioning mainnet blockchain.</p>
<h2 id="considerations">Considerations</h2>
<p>When going from mainnet to a test mainnet <em>(testnet from now on, just keep in mind that it is the actual mainnet blockchain that is in use)</em> there are two major concerns or factors to take into account:</p>
<h3 id="whatever-happens-on-the-testnet-shall-not-impact-mainnet">1 &gt; Whatever happens on the testnet shall not impact mainnet</h3>
<p>Isolating the testnet daemons from mainnet is of utmost importance and priority</p>
<ul>
<li>Use firewall rules to explicitly allow traffic from the other daemons that are going to be running</li>
<li>Ubuntu 16.04 UFW, very simple:</li>
</ul>
<pre><code>  $ ufw allow ssh
  $ allow from 1.1.1.1 to any port 11300
  $ ufw enable 
</code></pre>
<ul>
<li>Alternatively, or as well as, use hosting provider’s firewall</li>
<li>Another idea is to run the testnet offline completely, maybe you have access to a data centre and have idle machines.</li>
</ul>
<h3 id="difficulty-is-going-to-be-high-have-a-way-to-meet-it-and-then-reduce-it">2 &gt; Difficulty is going to be high, have a way to meet it and then reduce it</h3>
<p>If possible setup a mining pool, and prepare miners to mine. Depending on what is being tested this provides the opportunity to figure out and test the upgrade path for miners. This way clear messaging can be communicated ahead of time to smooth the transition.</p>
<p>Alternately hardcode the difficulty. Doing this has a major downside though, depending on mining power, block time is probably going to deviate from the projects target block time.</p>
<h2 id="ok-so-what-is-needed-to-create-this-testnet-and-prove-whatever-needs-to-be-tested">OK, so what is needed to create this testnet and prove whatever needs to be tested?</h2>
<ol>
<li><a href="#pick-a-ring-leader">Pick a ring leader!</a></li>
<li><a href="#create-a-space-pick-a-date-and-time">Create a space, pick a date and time</a></li>
<li><a href="#mainnet-blockchain-on-the-test-daemons">Mainnet blockchain on the test daemons</a></li>
<li><a href="#lists-of-daemons-ips--ports">Lists of daemons IPs &amp; ports</a></li>
<li><a href="#a-way-to-start-and-stop-things-preferably-automatedscripted">A way to start and stop things, preferably automated/scripted</a></li>
<li><a href="#monitoring-tools">Monitoring tools</a></li>
<li><a href="#mining-pools">Mining pool(s)</a></li>
<li><a href="#miner-strategy">Miner strategy</a></li>
</ol>
<h3 id="pick-a-ring-leader">1. Pick a ring leader!</h3>
<p>There can only be one ring leader once this task begins. They are responsible for what happens, do what they say. If you disagree with their direction, that’s fine, become a spectator. If you feel they are going to break mainnet raise it polielty, clearly and factually; drop all emotions. The rest of the group need stop everything and wait for this to play out, offer support where appropriate. <strong>Ensuring mainnet remains 100% operational is paramount</strong>, take this seriously!</p>
<h3 id="create-a-space-pick-a-date-and-time">2.  Create a space, pick a date and time</h3>
<p>A dedicated space needs to be created for this testnet event, and only those participating should have voice access. Allow spectators, always great to have community involvement, simply let them chat in the regular project channels. The ring leader needs clear communication lines to the other participants.</p>
<p>Secondly pick a suitable date and time and prepare in advance for things to kick off then. Test scripts, provision floating IPs, startup a Google Shell session and load up all tools and scripts to be ready, gather API tokens, etc.</p>
<h3 id="mainnet-blockchain-on-the-test-daemons">3. Mainnet blockchain on the test daemons</h3>
<p>Ideally this will be gotten very close in time from mainnet, the further away from the last block the testnet gets there will be an impact on the block time. For this reason everything should be scripted and automated, less likely to make a mistake as well. Making a mistake with this could break mainnet, ensuring mainnet remains 100% operational is paramount.</p>
<h3 id="list-of-daemons-ips--ports">4. List of daemons IPs &amp; ports</h3>
<p>Create a new channel / space to organise who is involved. This is super important, ensuring mainnet remains 100% operational is paramount! Everyone will need to supply their daemons IP &amp; ports. The ring leader will need to have already setup someway to ensure everyone has access to the list, a GitHub Gist is probably suitable.</p>
<p>Only IPs and ports on this list should be accepted on each of the running daemons. Make sure firewall rules are in place. This is SUPER important, if the code being tested communicates with mainnet <em>(remember the testnet is running the exact same blockchain network config and can communicate with mainnet!)</em>, mainnet could stop working. <strong>Ensuring mainnet remains 100% operational is paramount.</strong></p>
<h3 id="a-way-to-start-and-stop-things-preferably-automatedscripted">5. A way to start and stop things, preferably automated/scripted</h3>
<p>It doesn’t matter what tech is used for this, doing it by hand is way to prone to error. In the next section, <a href="#a-scripted-testnet">A scripted testnet</a>, one way is detailed in depth with a test procedure covering tools and tech used for the TurtleCoin PoW algorithm upgrade of April 2018 testnet.</p>
<h3 id="monitoring-tools">6. Monitoring tools</h3>
<h3 id="mining-pools">7. Mining pool(s)</h3>
<h3 id="miner-strategy">8. Miner strategy</h3>
<h2 id="a-scripted-testnet">A scripted testnet</h2>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

