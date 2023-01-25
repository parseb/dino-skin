<script>
  import {
    defaultEvmStores,
    connected,
    provider,
    chainId,
    chainData,
    signer,
    signerAddress,
    contracts,
  } from "svelte-ethers-store";
  import { ethers } from "ethers";
  import { element, onMount } from "svelte/internal";

  // import {
  //   ODAOABI
  // } from "./abi/ABIS";


  
  export const logIn = async () => {
    const p = new ethers.providers.Web3Provider(window.ethereum);
    const accounts = await p.send("eth_requestAccounts", []);
    const signer = p.getSigner();
    defaultEvmStores.setProvider(p);

    sessionStorage.setItem("loggedIn", "true");
    console.log(signerAddress);
  };

  export const logOut = async () => {
    sessionStorage.setItem("loggedIn", "false");
    defaultEvmStores.disconnect();
    // defaultEvmStores.setProvider(null);
    location.reload();
  };

  // == Logs ==
  // Member GOERLI ______________####_____ :  0x235626Da22545B86f14cf7bD76df92C838eFF038
  // ODAO GOERLI ______________####_____ :  0x33708a895CcDB9F3272EE3dA0c73edeC33Cd1D73
  // MembraneR ______________####_____ :  0xB2bD0180f5168693771176B61459c4FbEB2dab8b
  // MKR GOERLI  ______________####_____ :  0x3C157d0AD9033F2dCc96f8BeD94B07d6efada3E1


  ///  0xadb0e8d835d00c2ef762604b3a54d2dd611c5cff - m22
  /// 0x6C12dA1b89635367349543981Ea1Be2844e591AE - mkr mock 
 


  onMount(async () => {
    // add a test to return in SSR context
    let isLoggedIn = sessionStorage.getItem("loggedIn");
    if (isLoggedIn == "true") {
      await defaultEvmStores.setProvider();
      await defaultEvmStores.attachContract(
        "Member1155",
        "0x235626Da22545B86f14cf7bD76df92C838eFF038",
        MemberRegistryABI
      );
      await defaultEvmStores.attachContract(
        "ODAO",
        "0x33708a895CcDB9F3272EE3dA0c73edeC33Cd1D73",
        ODAOABI
      );
      await defaultEvmStores.attachContract(
        "MembraneRegistry",
        "0xB2bD0180f5168693771176B61459c4FbEB2dab8b",
        MemberaneRegistryABI
      );
    }
  });

  let prevElement;
</script>


<div class="container">
  <slot/>
</div>
<style>

</style>