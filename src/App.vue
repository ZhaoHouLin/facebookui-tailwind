
<script>
import { ref } from '@vue/reactivity'
import { onMounted } from 'vue'

export default {
  setup() {


    const plusBtn = ref()
    const msgBtn = ref()
    const notificationBtn = ref()
    const moreBtn = ref()

    const plusPanel = ref()
    const msgPanel = ref()
    const notificationPanel = ref()
    const morePanel = ref()

    const leftBlock = ref()
    const rightBlock = ref()

    const storyList = ref()

    const renderLeftItem = (name,imgUrl)=> {
      const leftItem =`
        <div
          class="
            flex
            items-center
            justify-items-center
            w-full
            p-2
            mb-1
            rounded
            hover:bg-fb-input
            cursor-pointer
          "
        >
          <div class="w-[32px] overflow-hidden rounded-full mr-4">
            <img src="${imgUrl}" alt="" />
          </div>
          <p class="text-white text-[.9rem]">${name}</p>
        </div>
      `
      return leftItem
    }

    const renderLeftBlock = ()=> {

      const leftArr = [
        {
          name: "Raiden",
          img: "https://bruce-fe-fb.web.app/image/avator.png",
        },
        {
          name: "活動",
          img: "https://bruce-fe-fb.web.app/image/left/activity.svg",
        },
        {
          name: "天氣",
          img: "https://bruce-fe-fb.web.app/image/left/cloudy.png",
        },
        {
          name: "災害應變中心",
          img: "https://bruce-fe-fb.web.app/image/left/dynamic.svg",
        },
        {
          name: "新冠病毒資訊中心",
          img: "https://bruce-fe-fb.web.app/image/left/facemask.svg",
        },
        {
          name: "社團",
          img: "https://bruce-fe-fb.web.app/image/left/friend.svg",
        },
        {
          name: "企業管理平台",
          img: "https://bruce-fe-fb.web.app/image/left/job.png",
        },
        {
          name: "Messenger",
          img: "https://bruce-fe-fb.web.app/image/left/messenger.svg",
        },
        {
          name: "近期廣告動態",
          img: "https://bruce-fe-fb.web.app/image/left/pay.png",
        },
        {
          name: "朋友名單",
          img: "https://bruce-fe-fb.web.app/image/left/sale.png",
        },
        {
          name: "最愛",
          img: "https://bruce-fe-fb.web.app/image/left/star.svg",
        },
        {
          name: "Marketplace",
          img: "https://bruce-fe-fb.web.app/image/left/store.svg",
        },
        {
          name: "Watch",
          img: "https://bruce-fe-fb.web.app/image/left/watchingTv.svg",
        },
      ];

      let htmlStr= ''

      leftArr.forEach(element => {
        htmlStr += renderLeftItem(element.name,element.img)
      });

      leftBlock.value.innerHTML = htmlStr
    }

    const renderRightItem = (name,imgUrl)=> {
      const rightItem = `
        <div
          class="
            flex
            items-center
            justify-items-center
            w-full
            py-2
            px-1
            rounded
            hover:bg-fb-input
            cursor-pointer
          "
        >
          <div class="w-[45px]">
            <div class="relative w-[32px] cursor-pointer">
              <div class="overflow-hidden rounded-full">
                <img src=${imgUrl} alt="" />
              </div>
              <div
                class="
                  w-[8px]
                  h-[8px]
                  rounded-full
                  bg-green-500
                  absolute
                  bottom-0
                  right-0
                  ring-gray-900 ring
                "
              ></div>
            </div>
          </div>
          <p class="text-white text-[.9rem]">${name}</p>
        </div>
      `
      return rightItem
    }

    const renderRightBlock = ()=> {

      const rightArr = [
        {
          name: "Raiden",
          img: "https://bruce-fe-fb.web.app/image/avator.png",
        }
      ];

      let htmlStr= '<p class="mb-2 text-lg text-gray-400">聯絡人</p>'

      for (let index = 0; index < 10; index++) {
        htmlStr += renderRightItem(rightArr[0].name,rightArr[0].img)
      }
      // rightArr.forEach(element => {
      //   htmlStr += renderRightItem(element.name,element.img)
      // });

      rightBlock.value.innerHTML = htmlStr
    }

    const renderStoryItem = ()=> {
      
      for (let index = 0; index < 5; index++) {
        const divBox = document.createElement('div')
        divBox.classList.add('flex-1','cursor-pointer','px-[4px]','min-w-[120px]')
        divBox.innerHTML = `
          <div class="relative overflow-hidden" id="story-${index}">
            <div id="story-mask-${index}" class="hidden absolute w-full h-full top-0 left-0 bg-black/20 z-20"></div>
            <div class="absolute top-4 left-4 ring-4 ring-fb bg-fb-card rounded-full flex justify-center items-center z-30 w-[32px] h-[32px]">
              <p class="text-white text-sm">R</p>
            </div>
            <div class="absolute w-full h-full top-0 left-0 bg-gradient-to-b to-transparent from-black/30 z-20"></div>
            <img id="story-image-${index}" class="w-full h-full duration-200 hover:scale-105" src="https://bruce-fe-fb.web.app/image/story.png" />
            <p class="absolute bottom-2 left-2 text-white">RaidenLin</p>
          </div>
        `

        divBox.addEventListener('mouseover',()=> {
          const mask = document.getElementById(`story-mask-${index}`)
          const image = document.getElementById(`story-image-${index}`)
          mask.classList.remove('hidden')
          image.classList.add('scale-105')
        })

        divBox.addEventListener('mouseout',()=> {
          const mask = document.getElementById(`story-mask-${index}`)
          const image = document.getElementById(`story-image-${index}`)
          mask.classList.add('hidden')
          image.classList.remove('scale-105')
        })

        storyList.value.appendChild(divBox)

      }

    }


    const panels = ref([plusPanel,msgPanel,notificationPanel,morePanel])

    const openPanel = (index,event)=> {
      // console.log(index,event);
      event.stopPropagation()
      panels.value.forEach((element,idx) => {
        if(index===idx) {
          element.value.classList.remove('hidden')
          return
        }
        if(element.value.classList.contains('hidden')) {
          return
        }
        element.value.classList.add('hidden')
      });
    }


    //取消傳遞window被點
    const panelStopPropagation= (e)=> {
      e.stopPropagation();
    }

    onMounted(() => {
      window.addEventListener('click',(event)=> {
        openPanel(-1,event)
        // console.log('window');
      })

      renderLeftBlock()
      renderRightBlock()
      renderStoryItem()
    })


    return {
      plusBtn,
      plusPanel,
      msgBtn,
      msgPanel,
      notificationBtn,
      notificationPanel,
      moreBtn,
      morePanel,
      panelStopPropagation,
      openPanel,
      leftBlock,
      rightBlock,
      storyList
    }
  }
}
</script>


<template lang='pug'>
header(class="w-full h-[56px] bg-fb-header fixed top-0 left-0 right-0 flex items-center justify-between px-4 z-20")

  //- header left
  div(class="flex items-center")
    svg.fill-current.text-fb(viewBox='0 0 36 36' height='39' width='39')
      defs
        lineargradient(x1='50%' x2='50%' y1='97.0782153%' y2='0%')
          stop(offset='0%' stop-color='#0062E0')
          stop(offset='100%' stop-color='#19AFFF')
      path(d='M15 35.8C6.5 34.3 0 26.9 0 18 0 8.1 8.1 0 18 0s18 8.1 18 18c0 8.9-6.5 16.3-15 17.8l-1-.8h-4l-1 .8z')
      path.fill-current.text-white(d='M25 23l.8-5H21v-3.5c0-1.4.5-2.5 2.7-2.5H26V7.4c-1.3-.2-2.7-.4-4-.4-4.1 0-7 2.5-7 7v4h-4.5v5H15v12.7c1 .2 2 .3 3 .3s2-.1 3-.3V23h4z')


    //- search bar (只在電腦版顯示)
    button.popover-btn(class='lg:hidden')
      img(src='https://bruce-fe-fb.web.app/image/search.svg')
    .bg-fb-input.ml-2.py-2.px-3.rounded-full.items-center.hidden(class='w-[240px] lg:flex')
      svg.mr-2(xmlns='http://www.w3.org/2000/svg' class='w-[18px] h-[18px]' fill='none' viewBox='0 0 24 24' stroke='#9ba3af')
        path(stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z')
      input.w-full.bg-transparent.text-white(type='text' class='focus:outline-none' placeholder='搜尋 Facebook')


  //- header right
  .flex.items-center.relative
    button#plus-btn.popover-btn(ref='plusBtn' @click='openPanel(0,$event)')
      img(src='https://bruce-fe-fb.web.app/image/plus.svg')
    button#msg-btn.popover-btn(ref='msgBtn' @click='openPanel(1,$event)')
      img(src='https://bruce-fe-fb.web.app/image/messenger.svg')
    button#notification-btn.popover-btn(ref='notificationBtn' @click='openPanel(2,$event)')
      img(src='https://bruce-fe-fb.web.app/image/bell.svg')
    button#more-btn.popover-btn(ref='moreBtn' @click='openPanel(3,$event)')
      img(src='https://bruce-fe-fb.web.app/image/down.svg' )
    
    //- plus
    #plus-panel.popover-panel.hidden(ref='plusPanel' @click='panelStopPropagation')
      p.text-white.mb-3.text-2xl 建立
      .flex.items-center.p-1.mb-2.rounded-lg.cursor-pointer(class='hover:bg-fb-input')
        .bg-fb-input.rounded-full.p-2.mr-2.flex.justify-center.items-center
          svg(xmlns='http://www.w3.org/2000/svg' fill='none' width='22' height='22' viewBox='0 0 24 24' stroke='white')
            path(stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z')
        .flex-1
          p.text-sm.text-white(class='mb-[2px]') 貼文
          p.text-xs.text-gray-400 在動態消息分享貼文。
    
    //- messenger
    #msg-panel.popover-panel.hidden(ref='msgPanel' @click='panelStopPropagation')
      p.text-white.mb-3.text-2xl Messsenger
      .bg-fb-input.rounded-full.py-1.px-3.flex.items-center.mb-4
        svg.mr-2(xmlns='http://www.w3.org/2000/svg' class='w-[18px] h-[18px]' fill='none' viewBox='0 0 24 24' stroke='#9ba3af')
          path(stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z')
        input.w-full.bg-transparent.text-white(type='text' class='focus:outline-none' placeholder='搜尋 Messsenger')
      .flex.items-center.mb-2.p-2.rounded-lg.cursor-pointer(class='hover:bg-fb-input')
        .rounded-full.overflow-hidden.mr-3(class='w-[50px] h-[50px]')
          img.w-full.object-cover(src='https://bruce-fe-fb.web.app/image/avator.png' alt='')
        .flex-1
          p.text-base.text-white(class='mb-[2px]') 布魯斯
          p.text-sm.text-gray-400 TailwindCSS讚讚！・1分鐘前
    
    //- notification
    #notification-panel.popover-panel.hidden(ref='notificationPanel' @click='panelStopPropagation')
      p.text-white.mb-3.text-2xl 通知
      .flex.items-center.mb-2.p-2.rounded-lg.cursor-pointer(class='hover:bg-fb-input')
        .rounded-full.overflow-hidden.mr-3(class='w-[50px] h-[50px]')
          img.w-full.object-cover(src='https://bruce-fe-fb.web.app/image/avator.png' alt='')
        .flex-1
          p.text-sm.text-white(class='mb-[2px]')
            | 布魯斯發佈了一門新課程！
          p.text-xs.text-fb 1分鐘前
    //- more      
    #more-panel.popover-panel.hidden(ref='morePanel' @click='panelStopPropagation')
      .flex.items-center.mb-2.p-2.rounded-lg.cursor-pointer(class='hover:bg-fb-input')
        .rounded-full.overflow-hidden.mr-3(class='w-[50px] h-[50px]')
          img.w-full.object-cover(src='https://bruce-fe-fb.web.app/image/avator.png' alt='')
        .flex-1
          p.text-base.text-white(class='mb-[2px]') 林炤后
          p.text-sm.text-gray-400 查看你的個人檔案
      .flex.p-1.mb-2.items-center.rounded-lg.cursor-pointer(class='hover:bg-fb-input')
        .bg-fb-input.rounded-full.p-2.mr-2.flex.justify-center.items-center
          svg(xmlns='http://www.w3.org/2000/svg' fill='none' width='22' height='22' viewBox='0 0 24 24' stroke='white')
            path(stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1')
        p.flex-1.text-white 登出
  
      

main(class="min-h-[100vh] pt-main-span flex")

  #left-block.hidden.sticky.top-main-span.w-full.h-full.pl-4(class='max-w-[360px] lg:block' ref='leftBlock')

  //- 限實動態
  div(class="max-w-[744px] w-full mx-auto px-4")
    .relative
      #story-list.flex.overflow-x-auto.no-scrollbar(ref='storyList')
        .flex-1.cursor-pointer(class='px-[4px] min-w-[120px]')
          .h-full.flex.flex-col
            .h-full.overflow-hidden
              img.object-cover.w-full.h-full.duration-500(class='hover:scale-105' src='https://bruce-fe-fb.web.app/image/avator.png')
            .bg-fb-card.pt-6.px-2.pb-2.relative
              button.p-2.absolute.-top-4.bg-fb.rounded-full.ring-fb-card.ring.flex.justify-center.items-center(class='w-[32px] h-[32px] left-[calc(50%-16px)] focus:outline-none')
                img(src='https://bruce-fe-fb.web.app/image/plus.svg')
              p.w-full.text-center.text-white 建立限時動態
        //- .relative.overflow-hidden(id='story-${index}')
        //-   .hidden.absolute.w-full.h-full.top-0.left-0.z-20(id='story-mask-${index}' class='bg-black/20')
        //-   .absolute.top-4.left-4.ring-4.ring-fb.bg-fb-card.rounded-full.flex.justify-center.items-center.z-30(class='w-[32px] h-[32px]')
        //-     p.text-white.text-sm R
        //-   .absolute.w-full.h-full.top-0.left-0.bg-gradient-to-b.to-transparent.z-20(class='from-black/30')
        //-   img.w-full.h-full.duration-200(id='story-image-${index}' class='hover:scale-105' src='https://bruce-fe-fb.web.app/image/story.png')
        //-   p.absolute.bottom-2.left-2.text-white RaidenLin


      button.absolute.popover-btn.-right-3.z-10(class='top-[calc(50%-22.5px)] w-[45px] h-[45px]')
        img(src='https://bruce-fe-fb.web.app/image/right-arrow.svg')


    //- 在想什麼
    .rounded-lg.mt-4.px-4.py-3.bg-fb-card
      .flex.pb-4
        .rounded-full.overflow-hidden.mr-3(class='w-[40px]')
          img(src='https://bruce-fe-fb.web.app/image/avator.png')
        .bg-fb-input.flex-1.rounded-full.flex.items-center
          p.text-left.text-sm.pl-3.text-gray-400
            | 布魯斯，在想些什麼？
      .border-t.border-gray-700.flex.pt-3
        button.flex-1.rounded-lg.flex.items-center.justify-center(class='h-[40px] hover:bg-fb-input')
          div(class='w-[16px]')
            img(src='https://bruce-fe-fb.web.app/image/camera.svg' alt='')
          p.text-gray-400.text-sm(class='pl-1.5') 直播視訊
        button.flex-1.rounded-lg.flex.items-center.justify-center(class='h-[40px] hover:bg-fb-input')
          div(class='w-[16px]')
            img(src='https://bruce-fe-fb.web.app/image/photo.svg' alt='')
          p.text-gray-400.text-sm(class='pl-1.5') 相片／影片
        button.flex-1.rounded-lg.flex.items-center.justify-center(class='h-[40px] hover:bg-fb-input')
          div(class='w-[16px]')
            img(src='https://bruce-fe-fb.web.app/image/feel.svg' alt='')
          p.text-gray-400.text-sm(class='pl-1.5') 感受／活動



  #right-block.hidden.sticky.top-main-span.w-full.h-full(class='max-w-[360px] lg:block' ref='rightBlock')
  //- #right-block.hidden.sticky.top-main-span.w-full.h-full(class='max-w-[360px] lg:block' ref='rightBlock' style='z-index: -1')

</template>

<style lang='stylus'>
#app 
  font-family Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  // text-align center
  color #2c3e50
  // margin-top 60px
  height 100vh

</style>
