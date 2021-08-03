<template>
  <div>
    <div class="header">
      <div class="logo">
        <a href="https://nindough.uwu.ai">
          <img src="@/assets/images/ndicon.svg" alt="" />
        </a>
        <h1><span>nindough</span></h1>
        <h6>alpha <span>1.0.0</span></h6>
      </div>

      <div class="nav-right">
        <div class="address" v-if="walletAccount">
          <a
            :href="`https://polygonscan.com/address/${walletAccount[0]}`"
            style="color: white;"
          >
            {{ walletAccount[0].substring(0, 6) }}...{{
              walletAccount[0].substring(38, 42)
            }}
          </a>
        </div>
        <div
          class="connect-address"
          v-if="!walletAccount"
          @click="reloadPage()"
        >
          <h5>Log in</h5>
        </div>
      </div>
    </div>
    <div
      class="close-button"
      @click="showSideMenu = true"
      style="z-index:100;"
      v-if="!showSideMenu"
    >
      <i class="ri-menu-unfold-line"></i>
    </div>
    <div class="side-bar" :class="{ active: showSideMenu }">
      <span
        @click="showSideMenu = false"
        class="close-button"
        style="position: relative; top: 0em; left: 7em;"
      >
        <i class="ri-menu-fold-line"></i>
      </span>
      <div
        style="position: absolute; top:2em; left: 2.1em; font-weight: 1000; color:#ffffff;"
      >
        <h2>Your ninjas. </h2>
      </div>
      <div
        style="position: absolute; top:6em; left: 2.1em; font-weight: 200; color:#ffffff;"
      >

        <p>The friend list will go here.</p>
      </div>
      <div style="position: absolute; top:12em; left: 2em; ">
        
        
      </div>
      <div style="position: absolute; bottom:3em; left: 2em; font-weight: 600;">
        <a href="https://quickchart.app/token/0xe718eda678aff3f8d1592e784652bcbeeb49e352">
          <img src="@/assets/images/ndicon.svg" style="width: 1.5em;" />
          <span style="color:#ffffff;"> ${{ otterPrice }}</span></a
        >
      </div>
      
    </div>

           
    <div class="container-fluid" 
    >
     
      <div class="row"
      >
        <div class="col-lg-12">
          <div
            class="card-transparent card-block card-stretch card-height mb-0"
          >
            <div class="d-flex justify-content-between">
              <div class="select-dropdown input-prepend input-append">
                <div class="btn-group">
                </div>
              </div>
            </div>
          </div>
        </div>
         
        <div class="col-lg-8">
          <div
            class="card card-block card-stretch card-height iq-welcome"
            
          >
            <div class="card-body property2-content">
              <div class="d-flex flex-wrap align-items-center">
                <div class="col-lg-10 col-sm-6 p-0">
                  <h4 class="mb-3" v-if="network == 1">
                           <img src="@/assets/images/icon/NDALERT.svg"
                          style="width:1.4em; margin-right: 0.1em;"/>
                    Please connect to the polygon mainnet to use nindough.
                    <a
                      href="https://medium.com/stakingbits/setting-up-metamask-for-polygon-matic-network-838058f6d844"
                      >Not sure how?</a
                    >
                  </h4>
                   
                  <h4 class="mb-3" v-if="network == 56">
                         <img src="@/assets/images/icon/NDALERT.svg"
                          style="width:1.4em; margin-right: 0.1em;"/>
                    Please connect to the polygon mainnet to use nindough.
                    <a
                      href="https://medium.com/stakingbits/setting-up-metamask-for-polygon-matic-network-838058f6d844"
                      >Not sure how?</a
                    >
                  </h4>


                  <h4 class="mb-3" v-if="network == 137">
                    <img src="@/assets/images/icon/NDLOGGEDIN.svg"
            style="width:1.4em; margin-right: 0.1em;"/>
                    You're now logged in. Use the buttons below to navigate the nindough dApp.
                  </h4>

                  <h4 class="mb-3"
                    v-if="
                      network &&
                        network !== 137 &&
                        network !== 56 &&
                        network !== 1">
                         <img src="@/assets/images/icon/NDALERT.svg"
                          style="width:1.4em; margin-right: 0.1em;"/>
                    Please connect to the polygon mainnet to use nindough.
                    <a
                      href="https://medium.com/stakingbits/setting-up-metamask-for-polygon-matic-network-838058f6d844"
                      >Not sure how?</a
                    >
                  </h4>
                  
                  <h4 class="mb-3" v-if="!network">
                    <img src="@/assets/images/icon/NDALERT.svg"
            style="width:1.4em; margin-right: 0.1em;"/>
                    Log in using Metamask. Not sure what that is?
                    <a href="https://blog.wetrust.io/how-to-install-and-use-metamask-7210720ca047"
                      >Learn more about metamask.</a>
                  </h4>
                </div>
              </div>
            </div>
          </div>
        </div>
      


      
        <div v-if="showUploadModal && walletAccount && network == 137" class="uploadModal">
          <div class="uploadModal__toolbar">
            <h4>Upload your File</h4>
            <h4 class="close" @click="showUploadModal = false">X</h4>
          </div>
          <UploadModal
            :Otter="Otter"
            :Pocket="Pocket"
            :myAddress="walletAccount[0]"
            :web3="web3"
            :fee="uploadFee"
          />
        </div>

        <div class="col-lg-8 col-xl-8" v-if="network == 137" >
          <div class="card card-block card-stretch card-height files-table">
            
            <div class=row>
             <div class="upload">
            <a  :href="`https://quickchart.app/token/0xe718eda678aff3f8d1592e784652bcbeeb49e352`">
            <img src="@/assets/images/NDB1EX.svg" style="width: 7.5em;" alt="Chart"/>
            </a>
          </div>
          <div class="upload">
            <a  :href="`https://quickchart.app/token/0xe718eda678aff3f8d1592e784652bcbeeb49e352`">
            <img src="@/assets/images/NDB5EX.svg" style="width: 7.5em;" alt="Chart"/>
            </a>
          </div>
          <div class="upload">
            <a  :href="`https://quickchart.app/token/0xe718eda678aff3f8d1592e784652bcbeeb49e352`">
            <img src="@/assets/images/NDB4EX.svg" style="width: 7.5em;" alt="Chart"/>
            </a>
          </div>
          <div class="upload">
            <a href="#" id="profile" @click="activeTab = 'PROFILE'">
            <img src="@/assets/images/NDB2EX.svg" style="width: 7.5em;" alt="Chart"/>
            </a>
          </div>
          <div class="upload">
            <a  :href="`https://quickchart.app/token/0xe718eda678aff3f8d1592e784652bcbeeb49e352`">
            <img src="@/assets/images/NDB3EX.svg" style="width: 7.5em;" alt="Chart"/>
            </a>
          </div>
          </div>
          </div>
        </div>
        <div id="over" class="{show : activeTab == 'OVER', hide : activeTab != 'OVER'}">
        <div class="col-lg-9">
          <div
            class="card card-block card-stretch card-height iq-welcome">
            <div class="card-body property2-content">
              <div class="d-flex flex-wrap align-items-center">
                <div class="col-lg-10 col-sm-6 p-0">
                  
        <h3 class="mb-3" v-if="network == 137">
                    <p><img src="@/assets/images/icon/NDICPROFILE.svg"
            style="width:10em; margin-right: -3.5em;"/>
                    Profile
                    </p>
                    <a>Profile section goes here.</a>
                  </h3>
                  </div>
                </div>
                </div>
            </div>
          </div>
        </div>


      </div>
      
    </div>
  </div>
</template>
<script>



import UploadModal from "../UploadModal.vue";
import Web3 from "web3";
import OtterToken from "../../../abi/Otter.json";
import OtterPocket from "../../../abi/Pocket.json";
import { convertBytes } from "./helpers";
import moment from "moment";
import "remixicon/fonts/remixicon.css";

export default {
  name: "Dashbord1",
  components: {
    UploadModal,
  },
  data() {
    return {
      showSideMenu: false,
      uploadFee: 0,
      otterPrice: 0.03,
      walletAccount: null,
      network: 0,
      polygonBalance: 0,
      otterBalance: 0,
      web3: null,
      Otter: null,
      Pocket: null,
      showUploadModal: false,
      fileCount: 0,
      Files: [],
      
      data: function () {
  return {
    activeTab: "OVER"
  }
}

    };
  },
  
  mounted() {
    this.loadWeb3();
  },
  methods: {
    convertBytes,
    date(date) {
      return moment.unix(date).format("h:mm:ss A M/D/Y");
    },
    reloadPage() {
      window.location.reload();
    },
    async loadWeb3() {
      if (window.ethereum) {
        window.web3 = new Web3(window.ethereum);
        this.web3 = window.web3;
        await window.ethereum.enable();
        this.network = await this.web3.eth.net.getId();

        this.walletAccount = await this.web3.eth.getAccounts();
        this.polygonBalance = await this.web3.eth.getBalance(
          this.walletAccount[0]
        );
        this.polygonBalance = this.web3.utils.fromWei(
          this.polygonBalance,
          "ether"
        );
        this.polygonBalance = parseFloat(this.polygonBalance);
        if (this.network == 137) {
          this.Otter = new this.web3.eth.Contract(
            OtterToken,
            "0xE718EDA678AFF3F8d1592e784652BcbEeb49e352"
          );
          this.Pocket = new this.web3.eth.Contract(
            OtterPocket,
            "0x501C5074bEd28987d50ce493018d7ccdE6B7C2d9"
          );
          this.otterBalance = this.web3.utils.fromWei(
            await this.Otter.methods.balanceOf(this.walletAccount[0]).call(),
            "ether"
          );
          this.otterBalance = parseFloat(this.otterBalance);
          this.otterBalance = this.otterBalance.toFixed(2);
          this.otterBalance = this.otterBalance.toLocaleString();

          const fileCount = await this.Pocket.methods
            .users(this.walletAccount[0])
            .call();
          this.uploadFee = await this.Pocket.methods.fee().call();
          this.fileCount = fileCount;
          // Load files&sort by the newest
          for (var i = this.fileCount; i >= 1; i--) {
            const response = await this.Pocket.methods
              .getFile(this.walletAccount[0], i)
              .call();
            console.log(response);

            let file = {
              fileId: response[0][0],
              fileSize: Number(response[0][1]),
              uploadTime: response[0][2],
              fileHash: response[1][0],
              fileType: response[1][1],
              fileName: response[1][2],
              fileDescription: response[1][3],
            };
            if (
              file.fileType.includes("png") ||
              file.fileType.includes("jpeg") ||
              file.fileType.includes("image")
            ) {
              file.fileIcon = "ri-image-line";
              file.fileColor = "icon-small rounded mr-3 bg-success";
            }
            if (
              file.fileType.includes("mp4") ||
              file.fileType.includes("mov") ||
              file.fileType.includes("video")
            ) {
              file.fileIcon = "ri-film-line";
              file.fileColor = " icon-small rounded mr-3 bg-danger";
            }
            if (
              file.fileType.includes("text") ||
              file.fileType.includes("application")
            ) {
              file.fileIcon = "far fa-file-alt";
              file.fileColor = "icon-small rounded mr-3 bg-warning";
            }
            this.Files.push(file);
          }
        }
      } else if (window.web3) {
        console.log(window.web3);
        window.web3 = new Web3(window.web3.currentProvider);
      } else {
        window.alert(
          "You need a browser capable of accessing BlockChain. Try Metamask plugin!"
        );
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.container-fluid {
  margin-top: -2em;
  
}
.upload {
  margin-top: 0.5em;
  margin-bottom: 2.5em;
  margin-left: 1.4em;
  margin-right: 0em;
  padding: 0em 0em;
  border-radius: 2em;
  background-size: 300% 100%;
  transition: all 0.4s ease-in-out;
  cursor: pointer;
  text-align: center;
  background-image: linear-gradient(
    to right,
    #6f4d9f,
    #6f4d9f,
    #63448e,
    #63448e
  );
  &:hover {
    background-position: 100% 0;
  }

  h4 {
    color: white;
  }
}
.uploadModal {
  top: 5em;
  position: fixed;
  width: 95vw;
  left: 2.5%;
  height: 80vh;
  box-shadow: 0 0 1rem 0 rgba(0, 0, 0, .2); 
  border-radius: 5px;
  background-color: rgba(255, 255, 255, .15);
  
  backdrop-filter: blur(10px);
  z-index: 9009;
  border-radius: 2em;
  &__toolbar {
    background: white;
    border-radius: 2em 2em 0 0;
    padding: 2em;
    display: flex;
    text-align: center;
    justify-content: space-between;
  }
}
.header {
  position: fixed;
  top: 0;
  height: 3.5em;
  left: 0;
  width: 100%;
  padding: 0 2em;
  display: flex;
  box-shadow: 0 0 1rem 0 rgba(0, 0, 0, .2); 
  border-radius: 5px;
  justify-content: space-between;
  background: linear-gradient(
    90deg,
    #6f4d9f 0%,
    #6f4d9f 20%,
    #6f4d9f 100%
  );
  z-index: 99;
}
.close-button {
  display: none;
  cursor: pointer;
  i {
    font-size: 2em;
    color: #46cdfd;
  }
}
.side-bar {
  position: fixed;
  left: 0px;
  top: 5em;
  width: 20.4em;
  height: calc(100% - 3em);
  //border: 4px solid #46cdfd;
  background: #6f4d9f;
  box-shadow: 0 0 1rem 0 rgba(0, 0, 0, .2); 
  border-radius: 5px;
  z-index: 99;
}
.connect-address {
  background: #6f4d9f;
  box-shadow: 0 0 1rem 0 rgba(0, 0, 0, .2); 
  border-radius: 10px;
  font-family: manrope;
  color: white;
  letter-spacing: 1px;
  height: 2em;
  padding: 0 2em;
  margin-top: 0.5em;
  border-radius: 1em;
}
.address {
  box-shadow: 0 0 1rem 0 rgba(0, 0, 0, .2); 
  border-radius: 5px;
  font-family: manrope;
  color: white;
  border-radius: 1em;

  height: 2em;
  padding: 0 2em;
  padding-top: 5px;
  margin-top: 0.75em;
}
.balance {
  margin-right: 1em;
  border: white 1px solid;
  color: white;
  border-radius: 1em;

  height: 2em;
  padding: 0 2em;
  margin-top: 0.5em;
}
.logo img {
  width:2em;
  margin-top: 0.75em;
  margin-left: 0em;
}
.connect-address:hover {
  background: #63448e;
  border: white 0px solid;
  cursor: pointer;
  color: white;
}
.nav-right {
  display: flex;
}
.close {
  cursor: pointer;
}
@media screen and (max-width: 1300px) {
  .side-bar {
    left: -10em;
    z-index: 99;
    top: 5.5em;
  }
  .side-bar.active {
    left: 0;
  }
  .close-button {
    display: inherit;
    position: fixed;
    top: 6em;
    left: 1em;
  }
}
@media screen and (max-width: 950px) {
  .header {
    flex-direction: column;
    height: 5.5em;
  }
  .address {
    font-size: 0.5em;
  }
  .balance {
    margin-bottom: 1em;
    font-size: 0.5em;
  }
}
</style>
