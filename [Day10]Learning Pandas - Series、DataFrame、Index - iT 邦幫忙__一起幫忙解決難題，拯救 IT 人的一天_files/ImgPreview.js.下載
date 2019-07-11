$(function() {
    var bs_modal =
        '<div class="modal fade" tabindex="-1" style=" min-height: 600px; height: 100%;">' +
        '<div class="modal-dialog" role="document" style="max-width: 1200px; width: 100%; text-align: center; top: 50%; transform: translateY(-70%);">' +
        '<img src="" style="max-width: 100%;">' +
        '</div>' +
        '</div>';

    $('.markdown__style').on('click', 'img', function() {
        var imgSrc = $(this).attr('src');
        var $bs_modal = $(bs_modal);
        $('body').append($bs_modal);
        $bs_modal.find('img').attr('src', imgSrc);
        $bs_modal.on('hidden.bs.modal', function(e) {
            $(this).remove();
        }).modal('show');
    });

    $('.markdown__style, .chatbox__markdown').find('a[href^="https://www.youtube.com/watch?v="]').has(
        'img[src^="http://img.youtube.com/vi/"]').each(function(i, elm) {
        $this = $(elm);
        var link = $this.attr('href');
        var bg_img_link = $this.find('img').attr('src');
        var youtube_ID = youtube_parser(link);
        $this[0].outerHTML = '<div style="background:url(' + bg_img_link +
            ') left no-repeat; font-size: 0;"><iframe width="480" height="360" src="https://www.youtube.com/embed/' +
            youtube_ID + '" frameborder="0" allowfullscreen></iframe></div>';
    });

    function youtube_parser(url) {
        var regExp = /^.*((youtu.be\/)|(v\/)|(\/u\/\w\/)|(embed\/)|(watch\?))\??v?=?([^#\&\?]*).*/;
        var match = url.match(regExp);
        return (match && match[7].length == 11) ? match[7] : url;
    }
})
