<template>
    <div class="parenthome">
        <div class="topPage">
            <button @click="formStatus = 'add'" class="modalBtn" id="modalBtn" v-if="formStatus !== 'add'">
                open modal form
            </button>
        </div>
        <div class="contentPage " v-if="formStatus !== 'close'">
            <div class="modalForm ">
                <div class="headerModal">
                    <div class="close " @click="formStatus = 'close' , getData()">
                        X
                    </div>
                </div>
                <div class="parentform">
                
                    <FormUsersForm :addUser="addUser" :userInfo="userInfo" :reset="reset" />
                </div>
            </div>
        </div>

        <!-- *********userList start***** -->

        <div id="mainList" class="margin" v-for="(item) of userList">
            <div class="userCard ">
                <div class="text">
           <p>
            my name is <span> {{ ' ' + item.firstName + ' ' + item.lastName + ' ' }} </span> , i am <span>{{
                        item.age
                    }}
                    </span> years old and i
                    am a <span> {{ item.job }} </span> , if you need to call me my phoneNumber is <span> {{ item.phoneNumber
                    }}</span>.
           </p>
                </div>
                <div class="cardBtn btnBox">
                    <button @click="formStatus = 'add', getuserInfo(item)" class="btn editBtn">edit</button>
                    <button class="btn deleteBtn" @click="deleteItem(item.id)">delete</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    // import axios from 'axios';
    data() {
        return {
            userList: [],
            formStatus: 'close',
            userInfo: {
                firstName: '', lastName: '', age: '', job: '', phoneNumber: ''
            }
        }
    },
    mounted() {
        this.getData()
    },
    methods: {
        getuserInfo(_item) {
            this.userInfo = _item
        },
        async getData() {
            let res = await this.$axios.$get(`http://localhost:2000/user`)
            this.userList = res
            this.reset()
        },
        async addUser(_userInfo) {
            let method = this.$axios.$post
            let route = 'http://localhost:2000/user/'
            if (_userInfo.id) {
                route += _userInfo.id
                method = this.$axios.$put
            }
            let res = await method(route, _userInfo)
            this.getData()
            this.formStatus = 'close'
        },
        async deleteItem(_id) {
            let res = await this.$axios.$delete(`http://localhost:2000/user/${_id}`)
            this.getData()
        },
        setFormStatus(_status) {
            this.formStatus = _status
        },
        reset() {
            this.userInfo = {
                firstName: '', lastName: '', age: '', job: '', phoneNumber: ''
            }
        }
    }
}
</script>
<style scoped>
.topPage {
    width: 100%;
    height: 100px;
    padding: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    /* border: 1px solid darkred; */
}

.contentPage {
    width: 100%;
    height: 500px;
    display: flex;
}

.modalBtn {
    border: none;
    width: 300px;
    height: 45px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgb(223, 130, 144);
    color: aliceblue;
    border-radius: 5px;
    transition: 0.5s;
}

.modalBtn:hover {
    box-shadow: rgb(223, 130, 144) 0px 0px 0px 2px, rgb(223, 130, 144) 0px 4px 6px -1px, rgb(223, 130, 144) 0px 1px 0px inset;
    background-color: aliceblue;
    color: rgb(223, 130, 144);
    font-weight: bolder;
}

.modalForm {
    width: 100% !important;
    height: 600px !important;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column !important;
    background-color: rgb(223, 130, 130);
}

.headerModal {
    width: 900px !important;
    height: 40px;
    display: flex;
    justify-content: start;
    align-items: center;
}

.headerModal>.close {
    width: 35px;
    height: 35px;
    border-radius: 5px;
    background-color: rgb(139, 0, 23);
    color: white;
    font-weight: bolder;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}

.parentform {
    width: 100%;
    height: 500px;

}

.headerModal>.close:hover {
    /* background-color: darkblue; */
    box-shadow: rgb(65, 0, 11) 0px 0px 0px 2px, rgb(65, 0, 11) 0px 4px 6px -1px, rgb(65, 0, 11) 0px 1px 0px inset;
    /* box-shadow: 1px 1px 1px rgb(145, 145, 181); */
}

.margin {
    margin-top: 100px !important;

}

.notMargin {
    margin-top: -100px !important;

}

#mainList {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px !important;
}

.userCard {
    width: 60% !important;
 
    height: 250px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    border-radius: 5px;
    color: gray;
    box-shadow: rgb(194, 0, 29) 0px 0px 5px 0px, rgb(194, 0, 29)0px 0px 1px 0px;
    transition: 0.5s;

}

.userCard:hover {
    box-shadow: rgb(194, 0, 29) 0px 0px 8px 0px, rgb(194, 0, 29) 0px 0px 5px 0px;

}
.userCard>div>p{
    padding: 20px !important;
    /* color: aqua; */
}
.userCard>div>p>span {
    color: rgb(45, 0, 7);
    font-weight: bolder;
}

.userCard>.text {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 20px;

}

.btnBox {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap !important;
    gap: 10px;
    margin-top: 10px;
    height: 10%;

}

.editBtn {
    width: 150px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgb(0, 69, 42);
    color: white;
    border-radius: 5px;
    transition: 0.5s;
}

.editBtn:hover {
    box-shadow: rgb(0, 69, 42) 0px 1px 3px, rgb(0, 69, 42) 0px 1px 2px;
    color: rgb(0, 69, 42);
    background-color: aliceblue;
    font-weight: bolder;
}

.deleteBtn {
    width: 150px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgb(232, 2, 2);
    color: white;
    border-radius: 5px;
    transition: 0.5s;
}

.deleteBtn:hover {
    box-shadow: rgb(232, 2, 2) 0px 1px 3px, rgb(232, 2, 2) 0px 1px 2px;
    color: rgb(232, 2, 2);
    background-color: aliceblue;
    font-weight: bolder;
}

/* ****userliststyle**** */
</style>