<template>
    <title>Buyer Dashboard | Produce Mart</title>
    <dash-sidebar/>
    <!--Main Content-->
    <section class="main_content dashboard_part large_header_bg">
        <dash-navbar/>

        <div class="main_content_iner overly_inner ">
            <div class="container-fluid p-0 ">
                <!--Breadcrumb-->
                <div class="row">
                    <div class="col-12">
                        <div class="dashboard_header mb_50">
                            <div class="row">
                                <div class="col-lg-8">
                                    <div class="dashboard_header_title">
                                        <h3>Buyer Dashboard</h3>
                                    </div>
                                </div>
                                <div class="col-lg-4">
                                    <div class="dashboard_breadcam text-right">
                                        <p>
                                            Dashboard
                                        </p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="row">
                    <!--Top 4 Boxes-->
                    <div class="col-lg-12 mb-5 text-center">
                        <div class="dashboardBannerBuyer">
                            <h1>Agricultural Product Delivered To Your Doorstep</h1>
                            <router-link to="/request-a-product"><a class="requestRoute">Request a Product <i class="bi bi-arrow-right"></i></a></router-link>
                        </div>
                    </div>
                    <!--Top 4 Boxes-->
                    <div class="col-lg-12">
                        <div class="white_card card_height_100 mb_30 user_crm_wrapper">
                            <div class="row">
                                <div class="col-lg-4">
                                    <div class="crm_box">
                                        <h4>{{items.total_order ?? 0}}</h4>
                                        <p>Total Orders</p>
                                        <img src="@/assets/img/dashboard-img/icon-buyer-totalorder.png" ondragstart="return false;">
                                    </div>
                                </div>
                                <div class="col-lg-4">
                                    <div class="crm_box">
                                        <h4>{{items.open_order ?? 0}}</h4>
                                        <p>Open Orders</p>
                                        <img src="@/assets/img/dashboard-img/icon-buyer-pendingorder.png" ondragstart="return false;">
                                    </div>
                                </div>
                                <div class="col-lg-4">
                                    <div class="crm_box">
                                        <h4>{{items.closed_order ?? 0}}</h4>
                                        <p>Closed Order</p>
                                        <img src="@/assets/img/dashboard-img/icon-buyer-orderhistory.png" ondragstart="return false;">
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <!--Table-->
                    <div class="col-lg-12">
                        <div class="white_card card_height_100 mb_30">
                            <div class="white_card_header">
                                <div class="box_header m-0">
                                </div>
                            </div>
                            <div class="white_card_body">
                                <div class="QA_section">
                                    <div class="white_box_tittle list_header">
                                    <h4>Recent Orders</h4>
                                    <div class="box_right d-flex lms_block">
                                        <div class="serach_field_2">
                                            <div class="search_inner">
                                                <form Active="#">
                                                <div class="search_field">
                                                    <input type="text" placeholder="Search content here...">
                                                </div>
                                                <button type="submit"><i class="bi bi-search"></i> </button>
                                                </form>
                                            </div>
                                        </div>
                                    </div>
                                    </div>
                                    <div class="QA_table mb_30">
                                    <table class="table">
                                        <thead>
                                            <tr>
                                                <th scope="col">#</th>
                                                <th scope="col">Order ID</th>
                                                <th scope="col">Product Name</th>
                                                <th scope="col">Quantity    </th>
                                                <th scope="col">Date</th>
                                                <th scope="col">Order Status</th>
                                            </tr>
                                        </thead>
                                        <tbody v-for="(item, i) in orderList" :key='item._id'>
                                            <tr>
                                                <th scope="row">{{i + 1}}</th>
                                                <td>{{item._id }}</td>
                                                <td><div v-if="item.quote.product !== null">{{item.quote.product.name }}</div></td>
                                                <td>{{item.quote.quantity || 0 }} <div v-if="item.quote.product !== null">{{item.quote.product.order.qty_unit }}</div></td>
                                                <td>{{getDate(item.createdAt)}}</td>
                                                <td>
                                                    <span v-if="item.status == 'open'">
                                                        <a href="#" class="status_await">Open</a>
                                                    </span>
                                                    <span v-if="item.status == 'closed'">
                                                        <a href="#" class="status_btn">Closed</a>
                                                    </span>
                                                </td>
                                            </tr>
                                            <!--<tr>
                                                <th scope="row">2</th>
                                                <td>Banana-BNL-324LL</td>
                                                <td>Banana</td>
                                                <td>2022--03-25</td>
                                                <td><a href="#" class="status_await">Awaiting Shipping</a></td>
                                            </tr>
                                            <tr>
                                                <th scope="row">3</th>
                                                <td>Oil-RBL-2029G</td>
                                                <td>Oil</td>
                                                <td>2022--03-20</td>
                                                <td><a href="#" class="status_btn-pending">Awaiting Delivery</a></td>
                                            </tr>
                                            <tr>
                                                <th scope="row">3</th>
                                                <td>Beans-WER-G29G</td>
                                                <td>Beans</td>
                                                <td>2022--03-10</td>
                                                <td><a href="#" class="status_btn">Delivered</a></td>
                                            </tr>-->
                                        </tbody>
                                    </table>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <!--Recent Notification-->
                    <!-- <div class="col-lg-3">
                        <div class="white_card card_height_100 mb_30">
                            <div class="white_card_header">
                                <div class="box_header m-0">
                                    <div class="main-title">
                                    <h3 class="m-0">Recent Notification</h3>
                                    </div>
                                    <div class="header_more_tool">
                                        <div class="dropdown">
                                            <span class="dropdown-toggle" id="dropdownMenuButton" data-bs-toggle="dropdown" aria-expanded="false">
                                                <i class="bi bi-three-dots"></i>
                                            </span>
                                            <div class="dropdown-menu dropdown-menu-right" aria-labelledby="dropdownMenuButton">
                                                <a class="dropdown-item" href="#"> <i class="bi bi-printer"></i> Print</a>
                                                <a class="dropdown-item" href="#"> <i class="bi bi-download"></i> Download</a>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="white_card_body">
                                <div class="Activity_timeline">
                                    <ul>
                                        <li>
                                            <div class="activity_bell"></div>
                                            <div class="timeLine_inner d-flex align-items-center">
                                                <div class="activity_wrap">
                                                    <h6>5 min ago</h6>
                                                    <p>You've gotten a new notification</p>
                                                </div>
                                            </div>
                                        </li>
                                        <li>
                                            <div class="activity_bell "></div>
                                            <div class="timeLine_inner d-flex align-items-center">
                                                <div class="activity_wrap">
                                                    <h6>5 min ago</h6>
                                                    <p>You've gotten a new notification</p>
                                                </div>
                                            </div>
                                        </li>
                                        <li>
                                            <div class="activity_bell "></div>
                                            <div class="timeLine_inner d-flex align-items-center">
                                                <div class="activity_wrap">
                                                    <h6>5 min ago</h6>
                                                    <p>You've gotten a new notification</p>
                                                </div>
                                            </div>
                                        </li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </div> -->
                </div>
            </div>
        </div>
        <dash-footer/>
    </section>
</template>
<style scoped src="@/assets/vendors/themefy_icon/themify-icons.css"></style>
<style scoped src="@/assets/vendors/niceselect/css/nice-select.css"></style>
<style scoped src="@/assets/css/style.css"></style>
<script>
    import DashSidebar from './dash-sidebar.vue'
    import DashNavbar from './dash-navbar.vue'
    import DashFooter from './dash-footer.vue'
    import axios from 'axios'
    
    export default {
      name: "Produce Mart",
      components:{
      'dash-sidebar': DashSidebar,
      'dash-navbar': DashNavbar,
      'dash-footer': DashFooter,
      },
      data(){
        return{
            user: JSON.parse(localStorage.getItem("user")) || '',
            orderSales: {
                quote: {
                    product: {
                        order: ''
                    }
                }
            },
            items: [],
            buyerId: '',
            orderList: [],
        }
      },
      methods: {
        getUser(){
            if (this.user.role == 'buyer'){
                this.buyerId = this.user._id
                this.getDashboard()
            }
        },
        getDate(value){
          return new Date(value).toLocaleDateString()
        },
        getDashboard(){
            axios.get(`https://producemart.herokuapp.com/buyerDashboard/${this.buyerId}?length=5`, {
                headers: {
                  "Content-Type": "application/json",
                  Authorization: this.user.token,
                },
            }).then(res => {
                //console.log(res.data)
                let dashData = res.data
                this.items = dashData
                this.orderList = dashData.orderlist
                this.orderSales = dashData.order_sales
            })
        }
      },
      mounted(){
        this.getUser();
            ////Scroll To Top
            window.scrollTo(0,0)
      }
    }
</script>