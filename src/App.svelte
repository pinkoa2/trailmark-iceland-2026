<script>
  import Banner from './lib/Banner.svelte'
  import Day from './lib/Day.svelte'

  const day1Photos = [
    { src: '/photos/day-1/rental-car.jpg', alt: 'Rental car', caption: 'Mazda CX-30' },
    { src: '/photos/day-1/blue-lagoon-arrival.jpg', alt: 'Blue Lagoon arrival', caption: 'Blue Lagoon' },
    { src: '/photos/day-1/blue-lagoon.jpg', alt: 'Blue Lagoon' },
    { src: '/photos/day-1/cityhub-reykjavik.jpg', alt: 'City Hub', caption: 'CityHub Reykjavik' },
    { src: '/photos/day-1/reykjavik-town.jpg', alt: 'Town' },
    { src: '/photos/day-1/hallgrimskirkja.jpg', alt: 'Cathedral', caption: 'Hallgrímskirkja' },
  ]

  const day2Photos = [
    { src: '/photos/day-2/oxararfoss.jpg', alt: 'Öxarárfoss', caption: 'Öxarárfoss' },
    { src: '/photos/day-2/waterfall.jpg', alt: 'Waterfall' },
    { src: '/photos/day-2/waterfall-video.mp4', alt: 'Waterfall', poster: '/photos/day-2/waterfall-video-poster.jpg' },
    { src: '/photos/day-2/bruarfoss.jpg', alt: 'Brúarfoss', caption: 'Brúarfoss' },
    { src: '/photos/day-2/strokkur-geyser.jpg', alt: 'Geysir field', caption: 'Strokkur Geyser' },
    { src: '/photos/day-2/strokkur-eruption.mp4', alt: 'Strokkur eruption', poster: '/photos/day-2/strokkur-eruption-poster.jpg' },
    { src: '/photos/day-2/boiling.mp4', alt: 'Boiling mud pot', poster: '/photos/day-2/boiling-poster.jpg' },
    { src: '/photos/day-2/gullfoss.jpg', alt: 'Gullfoss', caption: 'Gullfoss' },
    { src: '/photos/day-2/faxafoss.jpg', alt: 'Faxafoss', caption: 'Faxafoss' },
    { src: '/photos/day-2/kerid-crater.jpg', alt: 'Kerið Crater', caption: 'Kerið Crater' },
    { src: '/photos/day-2/aurora-igloo.jpg', alt: 'Aurora Igloo South', caption: 'Aurora Igloo South' },
  ]

  const day3Photos = [
    { src: '/photos/day-3/seljalandsfoss.jpg', alt: 'Seljalandsfoss', caption: 'Seljalandsfoss' },
    { src: '/photos/day-3/seljalandsfoss-behind.jpg', alt: 'Behind Seljalandsfoss' },
    { src: '/photos/day-3/gljufrabui.jpg', alt: 'Gljúfrabúi', caption: 'Gljúfrabúi' },
    { src: '/photos/day-3/gljufrabui-bridge.mp4', alt: 'Gljúfrabúi', poster: '/photos/day-3/gljufrabui-bridge-poster.jpg' },
    { src: '/photos/day-3/skogafoss-ting.jpg', alt: 'Skógafoss', caption: 'Skógafoss' },
    { src: '/photos/day-3/skogafoss-alex.jpg', alt: 'Skógafoss', caption: 'Skógafoss' },
    { src: '/photos/day-3/solheimasandur-plane-wreck.jpg', alt: 'Sólheimasandur Plane Wreck', caption: 'Sólheimasandur Plane Wreck' },
    { src: '/photos/day-3/skyrhusid-guesthouse.jpg', alt: 'Skyrhúsið Guesthouse', caption: 'Skyrhúsið Guesthouse' },
  ]

  const day4Photos = [
    { src: '/photos/day-4/dark-cave.jpg', alt: 'Ice cave' },
    { src: '/photos/day-4/both-ice-cave.jpg', alt: 'Ice cave' },
    { src: '/photos/day-4/ting-ice-cave.jpg', alt: 'Ice cave' },
    { src: '/photos/day-4/alex-blue-cave.jpg', alt: 'Blue ice cave' },
    { src: '/photos/day-4/glacier-crack.jpg', alt: 'Breiðamerkurjökull Glacier', caption: 'Breiðamerkurjökull Glacier' },
    { src: '/photos/day-4/glacier-ting.jpg', alt: 'Glacier' },
    { src: '/photos/day-4/diamond-beach.jpg', alt: 'Diamond Beach', caption: 'Diamond Beach' },
  ]

  const day5Photos = [
    { src: '/photos/day-5/reynisfjara-beach.jpg', alt: 'Reynisfjara Beach', caption: 'Reynisfjara Beach' },
    { src: '/photos/day-5/reynisfjara-beach-mountain.jpg', alt: 'Reynisfjara Beach' },
    { src: '/photos/day-5/reynisfjara-black-sand.jpg', alt: 'Reynisfjara black sand' },
    { src: '/photos/day-5/vik-church.jpg', alt: 'Vík í Mýrdal Church', caption: 'Vík í Mýrdal Church' },
    { src: '/photos/day-5/skool-beans.jpg', alt: 'Skool Beans', caption: 'Skool Beans' },
    { src: '/photos/day-5/skool-beans-inside.jpg', alt: 'Day 5' },
    { src: '/photos/day-5/yarn.jpg', alt: 'Day 5' },
  ]

  const day6Photos = [
    { src: '/photos/day-6/street-cat.jpg', alt: 'Street cat' },
    { src: '/photos/day-6/rainbow-street.jpg', alt: 'Rainbow street' },
    { src: '/photos/day-6/restaurant.jpg', alt: 'Restaurant' },
  ]

  let loadedThroughDay = $state(1)

  function markDayLoaded(day) {
    if (day === loadedThroughDay) {
      loadedThroughDay += 1
    }
  }
</script>

<Banner title="Iceland Trip 2026" src="/photos/banner.jpg" alt="Icelandic flag" />

<main>
  <Day
    dayNumber={1}
    title="Arrival & Blue Lagoon"
    description="We arrived at Keflavík Airport, picked up the rental car, and made our way to the Blue Lagoon. After dropping off our stuff at the hostel we were staying at, we explored the town of Reykjavík."
    mapEmbedUrl="https://www.google.com/maps/embed?pb=!1m40!1m12!1m3!1d447558.15650584997!2d-22.922364648597423!3d64.01193753511927!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!4m25!3e0!4m5!1s0x4929fdfce2ab799f%3A0x27f88d0a15c328cd!2sKeflav%C3%ADk%20International%20Airport%2C%20235%20Keflav%C3%ADk%2C%20Iceland!3m2!1d63.9814869!2d-22.6281862!4m5!1s0x48d603391e8fdb0f%3A0x120f680888c1cbd8!2sFlugvellir%2031%2C%20230%20Keflav%C3%ADk%2C%20Iceland!3m2!1d63.9970952!2d-22.5864379!4m5!1s0x48d61d66aff7df0d%3A0xf3747a894416f06e!2sBlue%20Lagoon%2C%20Nor%C3%B0urlj%C3%B3savegur%209%2C%20240%20Grindav%C3%ADk%2C%20Iceland!3m2!1d63.8807176!2d-22.4472964!4m5!1s0x48d6755fb0c858e9%3A0x44ada088622840f1!2sCityHub%20Reykjavik%2C%20Hverfisgata%2046%2C%20101%20Reykjav%C3%ADk%2C%20Iceland!3m2!1d64.1460424!2d-21.9276384!5e0!3m2!1sen!2sus!4v1787946049318!5m2!1sen!2sus"
    photos={day1Photos}
    active={loadedThroughDay >= 1}
    onloaded={() => markDayLoaded(1)}
  />
  <Day
    dayNumber={2}
    title="The Golden Circle"
    description="We drove the Golden Circle, stopping at Öxarárfoss, Brúarfoss, Strokkur Geyser, Gullfoss, Faxafoss, and Kerið Crater, and ended our day at an Aurora Borealis glass igloo."
    mapEmbedUrl="https://www.google.com/maps/embed?pb=!1m70!1m12!1m3!1d223220.31489224135!2d-21.35340771866608!3d64.08165706904842!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!4m55!3e0!4m5!1s0x48d6755fb0c858e9%3A0x44ada088622840f1!2sCityHub%20Reykjavik%2C%20Hverfisgata%2046%2C%20101%20Reykjav%C3%ADk%2C%20Iceland!3m2!1d64.1460424!2d-21.9276384!4m5!1s0x48d6811eadf0fd95%3A0x48dd72aa97e36e57!2s%C3%96xar%C3%A1rfoss%2C%207V8J%2B8RH%2C%20806%20Thingvellir%2C%20Iceland!3m2!1d64.2658062!2d-21.117884999999998!4m5!1s0x48d699b42950c4e9%3A0x2611ea18f9caca81!2zQnLDumFyZm9zcywgSGxhdXB0dW5nYSwgODA2IEJsw6Fza8OzZ2FieWdnw7AsIEljZWxhbmQ!3m2!1d64.2643026!2d-20.515746699999998!4m5!1s0x48d65fcb86a21e43%3A0x13fe408fd8ae0be3!2sStrokkur%20Geyser%2C%208M7X%2B3PJ%2C%20Hafnart%C3%BAn%2C%20806%20Selfoss%2C%20Iceland!3m2!1d64.3127094!2d-20.3007211!4m5!1s0x48d6a574af45b6c9%3A0x2c6347db0b411601!2sGullfoss%20Falls%2C%20846%2C%20Iceland!3m2!1d64.3270716!2d-20.1199478!4m5!1s0x48d6bd6a6b055599%3A0xd5bce6e9b4e2e516!2sFaxafoss%2C%20806%2C%20Iceland!3m2!1d64.225735!2d-20.3381288!4m5!1s0x48d68bb755f6f257%3A0x515a44e0c12ed907!2sKeri%C3%B0%20Crater%2C%20805%20Klausturholar%2C%20Iceland!3m2!1d64.04127849999999!2d-20.8851466!4m5!1s0x48d65f5cd78cafcd%3A0x43e27119d35c7e94!2sB%C3%B3nus%2C%20Larsenstr%C3%A6ti%205%2C%20800%20Selfoss%2C%20Iceland!3m2!1d63.9381675!2d-20.9737758!4m5!1s0x48d6fb180a637953%3A0x6b6b3ab62470f4e1!2sAurora%20Igloo%20South%2C%20Stekkat%C3%BAn%201%2C%20851%20Hella%2C%20Iceland!3m2!1d63.835106399999994!2d-20.421586299999998!5e0!3m2!1sen!2sus!4v1787947243205!5m2!1sen!2sus"
    photos={day2Photos}
    active={loadedThroughDay >= 2}
    onloaded={() => markDayLoaded(2)}
  />
  <Day
    dayNumber={3}
    title="South Coast Waterfalls"
    description="We visited Seljalandsfoss, Gljúfrabúi, and Skógafoss waterfalls, hiked out to the Sólheimasandur Plane Wreck, grabbed pizza in Vík, and ended the day at Skyrhúsið Guesthouse."
    mapEmbedUrl="https://www.google.com/maps/embed?pb=!1m58!1m12!1m3!1d902869.6840842406!2d-19.537457796881515!3d63.769759494687136!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!4m43!3e0!4m5!1s0x48d6fb180a637953%3A0x6b6b3ab62470f4e1!2sAurora%20Igloo%20South%2C%20Stekkat%C3%BAn%201%2C%20851%20Hella%2C%20Iceland!3m2!1d63.835106399999994!2d-20.421586299999998!4m5!1s0x48d71eade8ef2415%3A0xae01e6205209178d!2sSeljalandsfoss%2C%20861%2C%20Iceland!3m2!1d63.615623199999995!2d-19.9885688!4m5!1s0x48d71eb01553b317%3A0x966a55b6ec145f2e!2zR2xqw7pmcmFiw7ppLCAyNDksIDg2MSwgSWNlbGFuZA!3m2!1d63.620863099999994!2d-19.9864486!4m5!1s0x48d73b7639a58c15%3A0xf60c71fcdfe7948!2sSk%C3%B3gafoss%2C%20861%2C%20Iceland!3m2!1d63.5320523!2d-19.511370499999998!4m5!1s0x48d739a755286129%3A0xedc60e1d7a9cb464!2sSolheimasandur%20Plane%20Wreck%2C%20Path%20to%20Wrecked%20DC-3%20Plane%20on%20S%C3%B3lheimasandur%2C%20871%2C%20Iceland!3m2!1d63.459103999999996!2d-19.364789!4m5!1s0x48d74b361a8aa385%3A0xbae403cd3a0a1ac6!2sBlack%20Crust%20Pizzeria%2C%20Austurvegur%2016%2C%20870%20Vik%2C%20Iceland!3m2!1d63.4176685!2d-19.002747499999998!4m5!1s0x48cfd204c28a3b7b%3A0xc0d8f68f87d104ae!2zU2t5cmjDunNpw7AgR3Vlc3Rob3VzZSwgSGFsaSAzLCA3ODEgSG9ybmFmasO2csOwdXIsIEljZWxhbmQ!3m2!1d64.1294078!2d-16.0160555!5e0!3m2!1sen!2sus!4v1787950270817!5m2!1sen!2sus"
    photos={day3Photos}
    active={loadedThroughDay >= 3}
    onloaded={() => markDayLoaded(3)}
  />
  <Day
    dayNumber={4}
    title="Glacier Ice Caves"
    description="A 6-hour hike on the glacier to explore blue ice caves. We made our way back to Vík, stopping at Diamond Beach along the way."
    mapEmbedUrl="https://www.google.com/maps/embed?pb=!1m34!1m12!1m3!1d451374.0768888408!2d-18.172832520320696!3d63.773559396684966!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!4m19!3e0!4m5!1s0x48cfd204c28a3b7b%3A0xc0d8f68f87d104ae!2zU2t5cmjDunNpw7AgR3Vlc3Rob3VzZSwgSGFsaSAzLCA3ODEgSG9ybmFmasO2csOwdXIsIEljZWxhbmQ!3m2!1d64.1294078!2d-16.0160555!4m5!1s0x48cfd719a4fb06f3%3A0x4202e865f907845a!2sDiamond%20Beach%2C%20781%2C%20Iceland!3m2!1d64.04433399999999!2d-16.1776622!4m5!1s0x48d74a381786058f%3A0xa6686a4ab75afa86!2sSmi%C3%B0jan%20Bruggh%C3%BAs%2C%20Sunnubraut%2015%2C%20870%20V%C3%ADk%2C%20Iceland!3m2!1d63.4172849!2d-19.0109195!5e0!3m2!1sen!2sus!4v1787952787658!5m2!1sen!2sus"
    photos={day4Photos}
    active={loadedThroughDay >= 4}
    onloaded={() => markDayLoaded(4)}
  />
  <Day
    dayNumber={5}
    title="Reynisfjara & Vík"
    description="We visited the town of Vík, grabbing crepes, coffee, and doing some local shopping. Then we made our way back to Reykjavík."
    mapEmbedUrl="https://www.google.com/maps/embed?pb=!1m46!1m12!1m3!1d546934.5004776113!2d-20.345308171303692!3d63.89014681374215!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!4m31!3e0!4m5!1s0x48d74a0464df88db%3A0xd677ad29c8c3fc22!2sThe%20Barn%2C%20Nor%C3%B0urfoss%2C%20871%2C%20Iceland!3m2!1d63.4359359!2d-19.0622501!4m5!1s0x48d74984d567267d%3A0xe07954a3f4b36bd5!2sReynisfjara%20Beach%2C%20Iceland!3m2!1d63.4057404!2d-19.0716193!4m5!1s0x48d74bc91a292edf%3A0x201541c27078f6a6!2sSkool%20Beans%2C%20M%C3%B3sastallur%2C%20870%20Vik%2C%20Iceland!3m2!1d63.4203031!2d-18.981325599999998!4m5!1s0x48d74a4658732b83%3A0x46d27b299623a20d!2sV%C3%ADk%20i%20Myrdal%20Church%2C%20Sunnubraut%207%2C%20870%20Vik%2C%20Iceland!3m2!1d63.420501699999996!2d-19.0028796!4m5!1s0x48d60b33aa331a3d%3A0xf0812cb183ae4efd!2sGuesthouse%20Galtafell%2C%20Lauf%C3%A1svegur%2046%2C%20101%20Reykjav%C3%ADk%2C%20Iceland!3m2!1d64.14131189999999!2d-21.9369935!5e0!3m2!1sen!2sus!4v1787953511015!5m2!1sen!2sus"
    photos={day5Photos}
    active={loadedThroughDay >= 5}
    onloaded={() => markDayLoaded(5)}
  />
  <Day
    dayNumber={6}
    title="Last Day in Reykjavík"
    description="A relaxed, slow day — shopping, lots of bakeries, and enjoying our last day in Iceland."
    noMap
    photos={day6Photos}
    active={loadedThroughDay >= 6}
    onloaded={() => markDayLoaded(6)}
  />
  <Day
    dayNumber={7}
    title="Heading Home"
    description="Headed back to Keflavík Airport for our flight home, wrapping up an unforgettable trip."
    noMap
  />
</main>
