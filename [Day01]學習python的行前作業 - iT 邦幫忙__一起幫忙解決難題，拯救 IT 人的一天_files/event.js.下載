$(function () {
    window.mobilecheck = function () {
        var check = false;
        (function (a) {
            if (
                /(android|bb\d+|meego).+mobile|avantgo|bada\/|blackberry|blazer|compal|elaine|fennec|hiptop|iemobile|ip(hone|od)|iris|kindle|lge |maemo|midp|mmp|mobile.+firefox|netfront|opera m(ob|in)i|palm( os)?|phone|p(ixi|re)\/|plucker|pocket|psp|series(4|6)0|symbian|treo|up\.(browser|link)|vodafone|wap|windows ce|xda|xiino/i
                .test(a) ||
                /1207|6310|6590|3gso|4thp|50[1-6]i|770s|802s|a wa|abac|ac(er|oo|s\-)|ai(ko|rn)|al(av|ca|co)|amoi|an(ex|ny|yw)|aptu|ar(ch|go)|as(te|us)|attw|au(di|\-m|r |s )|avan|be(ck|ll|nq)|bi(lb|rd)|bl(ac|az)|br(e|v)w|bumb|bw\-(n|u)|c55\/|capi|ccwa|cdm\-|cell|chtm|cldc|cmd\-|co(mp|nd)|craw|da(it|ll|ng)|dbte|dc\-s|devi|dica|dmob|do(c|p)o|ds(12|\-d)|el(49|ai)|em(l2|ul)|er(ic|k0)|esl8|ez([4-7]0|os|wa|ze)|fetc|fly(\-|_)|g1 u|g560|gene|gf\-5|g\-mo|go(\.w|od)|gr(ad|un)|haie|hcit|hd\-(m|p|t)|hei\-|hi(pt|ta)|hp( i|ip)|hs\-c|ht(c(\-| |_|a|g|p|s|t)|tp)|hu(aw|tc)|i\-(20|go|ma)|i230|iac( |\-|\/)|ibro|idea|ig01|ikom|im1k|inno|ipaq|iris|ja(t|v)a|jbro|jemu|jigs|kddi|keji|kgt( |\/)|klon|kpt |kwc\-|kyo(c|k)|le(no|xi)|lg( g|\/(k|l|u)|50|54|\-[a-w])|libw|lynx|m1\-w|m3ga|m50\/|ma(te|ui|xo)|mc(01|21|ca)|m\-cr|me(rc|ri)|mi(o8|oa|ts)|mmef|mo(01|02|bi|de|do|t(\-| |o|v)|zz)|mt(50|p1|v )|mwbp|mywa|n10[0-2]|n20[2-3]|n30(0|2)|n50(0|2|5)|n7(0(0|1)|10)|ne((c|m)\-|on|tf|wf|wg|wt)|nok(6|i)|nzph|o2im|op(ti|wv)|oran|owg1|p800|pan(a|d|t)|pdxg|pg(13|\-([1-8]|c))|phil|pire|pl(ay|uc)|pn\-2|po(ck|rt|se)|prox|psio|pt\-g|qa\-a|qc(07|12|21|32|60|\-[2-7]|i\-)|qtek|r380|r600|raks|rim9|ro(ve|zo)|s55\/|sa(ge|ma|mm|ms|ny|va)|sc(01|h\-|oo|p\-)|sdk\/|se(c(\-|0|1)|47|mc|nd|ri)|sgh\-|shar|sie(\-|m)|sk\-0|sl(45|id)|sm(al|ar|b3|it|t5)|so(ft|ny)|sp(01|h\-|v\-|v )|sy(01|mb)|t2(18|50)|t6(00|10|18)|ta(gt|lk)|tcl\-|tdg\-|tel(i|m)|tim\-|t\-mo|to(pl|sh)|ts(70|m\-|m3|m5)|tx\-9|up(\.b|g1|si)|utst|v400|v750|veri|vi(rg|te)|vk(40|5[0-3]|\-v)|vm40|voda|vulc|vx(52|53|60|61|70|80|81|83|85|98)|w3c(\-| )|webc|whit|wi(g |nc|nw)|wmlb|wonu|x700|yas\-|your|zeto|zte\-/i
                .test(a.substr(0, 4))) check = true
        })(navigator.userAgent || navigator.vendor || window.opera);
        return check;
    }

    if (mobilecheck()) {
        var href = location.href;
        var origin = location.origin;
        var mobileLink = href.replace(origin, origin + '/m');
        location.href = mobileLink;
    }

    $(document).on('click', '.like_btn', function () {
        var $this = $(this);
        var id = $this.data('id');
        var type = $this.data('type');
        var nowNumber = parseInt($this.next('.likeGroup__num').text(), 10);

        // 前端先切換 class 及計數
        if ($this.hasClass('likeGroup__arrow--active')) {
            nowNumber--;
        } else {
            nowNumber++;
        }
        $this.next('.likeGroup__num').text(nowNumber);
        $this.toggleClass('likeGroup__arrow--active');

        $.post('/api/like', {
            'id': id,
            'type': type
        }, function (result) {
            if (result.status == "success") {
                // api 呼叫成功再 render 正確的數字
                $this.next('.likeGroup__num').text(result.data.amount);
                // $this.toggleClass('likeGroup__arrow--active');
                // sweetAlert('success', result.data.message, 'success');
            } else {
                if (result.errorCode == 706) {
                    window.location.replace("/users/login");
                } else {
                    // sweetAlert('failed', result.errorMsg, 'error');
                }
            }
        });
    });

    $(document).on('click', '.collection_btn', function () {
        var $this = $(this);
        var id = $this.data('id');
        var type = $this.data('type');
        $.post('/api/collection', {
            'id': id,
            'type': type
        }, function (result) {
            if (result.status == "success") {
                $this.toggleClass('collection__btn--active');
                $this.find('i').toggleClass('fa-star-o fa-star');
                // sweetAlert('success', result.data.message, 'success');
            } else {
                if (result.errorCode == 706) {
                    window.location.replace("/users/login");
                } else {
                    // sweetAlert('failed', result.errorMsg, 'error');
                }
            }
        });
    });

    $(document).on('click', '.subscription-btn', function () {
        var $this = $(this);
        var id = $this.data('id');
        var type = $this.data('type');
        $.post('/api/collection', {
            'id': id,
            'type': type
        }, function (result) {
            if (result.status == "success") {
                $this.toggleClass('active');
                $this.find('i').toggleClass('fa-bookmark-o fa-bookmark');
                // sweetAlert('success', result.data.message, 'success');
                var text = '訂閱系列文';
                if (result.data.message == 'Created') {
                    text = '已訂閱系列文';
                }

                $this.parent('.subscription-group')
                    .find('.subscription-amount').text(result.data.amount).end()
                    .find('.subscription-text').text(text);

            } else {
                if (result.errorCode == 706) {
                    window.location.replace("/users/login");
                } else {
                    // sweetAlert('failed', result.errorMsg, 'error');
                }
            }
        });
    });

    $(document).on('click', '.trace_btn', function () {
        var $this = $(this);
        var id = $this.data('id');
        var type = $this.data('type');
        $.post('/api/trace', {
            'id': id,
            'type': type
        }, function (result) {
            if (result.status == "success") {
                $this.toggleClass('qa-action__trace--active');
                $this.find('i').toggleClass('fa-heart-o fa-heart');
                // sweetAlert('success', result.data.message, 'success');
                $this.find('.amount').text(result.data.amount);
            } else {
                if (result.errorCode == 706) {
                    window.location.replace("/users/login");
                } else {
                    // sweetAlert('failed', result.errorMsg, 'error');
                }
            }
        });
    });

    // ========== comment
    $(document).on('click', '.edit_btn', function () {
        var $this = $(this);
        var $commentBody = $this.parents('.comment__body');
        var $commentContent = $commentBody.find('.comment__content');
        var $commentForm = $commentBody.find('.comment__form');
        $commentContent.toggle();
        $commentForm.toggle();
    });

    $(document).on('click', '.comment__form .comment__submit', function () {
        var $this = $(this);
        var $commentBody = $this.parents('.comment__body');
        var $commentContent = $commentBody.find('.comment__content');
        var $commentTextarea = $commentBody.find('.comment__textarea');
        var $commentForm = $commentBody.find('.comment__form');
        var description = $commentTextarea.val();
        var useMarkdown = $commentTextarea.hasClass('SimpleMDE');
        if (useMarkdown) {
            description = $commentTextarea.data('simplemde').value();
        }
        var ajaxUrl = $this.data('ajax');
        $.post(ajaxUrl, {
            description: description
        }).then(function (result) {
            if (result.status === 'success') {
                $commentContent.html(result.data.description);
                if (useMarkdown) {
                    $commentContent.html(result.data.description);
                }
                $commentContent.toggle();
                $commentForm.toggle();
            }
        });
    });

    // ========== answer
    $(document).on('click', '.answerEdit', function () {
        var $this = $(this);
        var $qaContent = $this.parents('.qa-panel__content');
        var $qaForm = $qaContent.find('.form-group');
        var $markdown = $qaContent.find('.markdown .markdown__style')
        var simplemde = $qaForm.find('textarea').data('simplemde');
        $markdown.toggle();
        $qaForm.toggle();
        setTimeout(function () {
            simplemde.codemirror.refresh();
        }, 100);
    });

    $(document).on('click', '.answerSubmit', function () {
        var $this = $(this);
        var $qaContent = $this.parents('.qa-panel__content');
        var $qaForm = $qaContent.find('.form-group');
        var $markdown = $qaContent.find('.markdown .markdown__style');
        var simplemde = $qaForm.find('textarea').data('simplemde');
        var markdown_text = simplemde.value();
        var ajaxUrl = $this.data('ajax');
        $.post(ajaxUrl, {
            description: markdown_text
        }).then(function (result) {
            if (result.status === 'success') {
                $markdown.html(result.data.description);
                $markdown.toggle();
                $qaForm.toggle();
            }
        });
    });
    // ========== response
    $(document).on('click', '.responseEdit', function () {
        var $this = $(this);
        var $qaContent = $this.parents('.qa-panel__content');
        var $qaForm = $qaContent.find('.form-group');
        var $markdown = $qaContent.find('.markdown .markdown__style');
        var simplemde = $qaForm.find('textarea').data('simplemde');
        $markdown.toggle();
        $qaForm.toggle();
        setTimeout(function () {
            simplemde.codemirror.refresh();
        }, 100);
    });

    //

    $(document).on('click', '.responseSubmit', function () {
        var $this = $(this);
        var $qaContent = $this.parents('.qa-panel__content');
        var $qaForm = $qaContent.find('.form-group');
        var $markdown = $qaContent.find('.markdown .markdown__style')
        var simplemde = $qaForm.find('textarea').data('simplemde');
        var markdown_text = simplemde.value();
        var ajaxUrl = $this.data('ajax');
        $.post(ajaxUrl, {
            description: markdown_text
        }).then(function (result) {
            if (result.status === 'success') {
                $markdown.html(result.data.description);
                $markdown.show();
                $qaForm.hide();
            }
        });
    });
    // ==========

    $(document).on('click', '.trace_btn_border', function () {
        var $this = $(this);
        var id = $this.data('id');
        var type = $this.data('type');
        $.post('/api/trace', {
            'id': id,
            'type': type
        }, function (result) {
            if (result.status == "success") {
                $this.toggleClass('btn-trace--active');
                $this.find('i').toggleClass('fa-heart-o fa-heart');
                $this.parent()
                    .find('.trace_num').text(result.data.amount).end()
                    .find('.taginfo__follow-num').text(result.data.amount);
                // sweetAlert('success', result.data.message, 'success');
            } else {
                if (result.errorCode == 706) {
                    window.location.replace("/users/login");
                } else {
                    // sweetAlert('failed', result.errorMsg, 'error');
                }
            }
        });
    });


    $(document).on('input propertychange', '.report_desc', function () {
        var $this = $(this);
        var num_length = $this.val().length;
        var $report_desc_length = $('#report_desc_length');
        $report_desc_length.text(num_length);
        if (num_length > 150) {
            $report_desc_length.css('color', 'rgb(255, 0, 0, .65)');
        } else {
            $report_desc_length.css('color', 'rgb(0, 0, 0, .65)');
        }
    });

    $(document).on('click', '.report_btn, .report_talk_btn', function () {
        var $this = $(this);
        var id = $this.data('id');
        var type = $this.data('type');
        $.post('/api/isReported', {
            'id': id,
            'type': type
        }, function (result) {
            if (result.status == "success") {
                if (result.data.is_reported) {
                    sweetAlert('錯誤訊息', '無法重複檢舉', 'error');
                } else {
                    sweetAlert({
                        title: '檢舉項目',
                        type: 'warning',
                        icon: "warning",
                        buttons: true,
                        buttons: ["取消檢舉", {
                            text: "確定檢舉",
                            className: "swal-button--warning",
                            closeModal: false,
                        }],
                        content: $.parseHTML('<div class="report_option">' + [
                            '<input type="radio" class="radio-input" name="report_option" value="crib" id="report_option1"><label for="report_option1" class="radio-label">抄襲</label>',
                            '<input type="radio" class="radio-input" name="report_option" value="porn" id="report_option2"><label for="report_option2" class="radio-label">色情</label>',
                            '<input type="radio" class="radio-input" name="report_option" value="advertisement" id="report_option3"><label for="report_option3" class="radio-label">廣告</label>',
                            '<input type="radio" class="radio-input" name="report_option" value="other" id="report_option4"><label for="report_option4" class="radio-label">其他</label>',
                        ].join('') + '</div>')[0]
                    }).then(function (value) {
                        if (!!value) {
                            var $this = $('.report_option > .radio-input:checked');
                            var value = $this.val();
                            return value;
                        } else {
                            sweetAlert.close();
                        }
                    }).then(function (report_type) {
                        if (!!report_type === false) {
                            sweetAlert.close();
                        } else if (report_type == 'crib' || report_type == 'other') {
                            var report_title = '檢舉抄襲'
                            var report_textarea = '請提供抄襲相關的資訊，例如抄襲的來源、內容…'
                            if (report_type == 'other') {
                                report_title = '檢舉其他'
                                report_textarea = '請告知提出檢舉的原因…'
                            }
                            sweetAlert({
                                title: report_title,
                                type: 'warning',
                                buttons: true,
                                buttons: ["取消檢舉", {
                                    text: "確定檢舉",
                                    className: "swal-button--warning",
                                    closeModal: false,
                                }],
                                content: $.parseHTML('<div>' + [
                                    '<p class="text-left" style="color:rgba(0,0,0,.65);">發生了什麼事</p>',
                                    '<textarea class="report_desc form-control" name="report_desc" maxlength="150" placeholder="' + report_textarea + '"></textarea>',
                                    '<p class="text-right" style="color:rgba(0,0,0,.65);">剩餘字數: <span id="report_desc_length">0</span>/150</p>'
                                ].join('') + '</div>')[0]
                            }).then(function (isConfirm) {
                                if (!!isConfirm) {
                                    var $this = $('.report_desc');
                                    var report_desc = $this.val();
                                    if (!!report_desc) {
                                        $.post('/api/report', {
                                            'id': id,
                                            'type': type,
                                            'report_type': report_type,
                                            'report_desc': report_desc
                                        }, function (result) {
                                            if (result.status == "success") {
                                                sweetAlert({
                                                    title: "感謝回報",
                                                    text: "感謝您的提報，我們將進行後續處理。",
                                                    icon: "success",
                                                    button: "關閉"
                                                });
                                            } else {
                                                sweetAlert('檢舉失敗', result.errorMsg.join('\n'), 'error');
                                            }
                                        });
                                    } else {
                                        sweetAlert({
                                            text: "請告知提出檢舉的原因",
                                            icon: "warning",
                                            button: "關閉"
                                        });
                                    }
                                } else {
                                    sweetAlert.close();
                                }
                            });
                        } else {
                            $.post('/api/report', {
                                'id': id,
                                'type': type,
                                'report_type': report_type,
                                'report_desc': ''
                            }, function (result) {
                                if (result.status == "success") {
                                    sweetAlert({
                                        title: "感謝回報",
                                        text: "感謝您的提報，我們將進行後續處理。",
                                        icon: "success",
                                        button: "關閉"
                                    });
                                } else {
                                    sweetAlert({
                                        title: "檢舉失敗",
                                        text: "",
                                        icon: "error",
                                        button: "關閉"
                                    });
                                }
                            });
                        }
                    });
                }
            } else {
                // sweetAlert('', result.errorMsg, 'warning');
                sweetAlert({
                    text: result.errorMsg,
                    icon: "warning",
                    button: "關閉"
                });
            }
        });
    });

    $(document).on('click', '.useless_answer_btn', function () {
        var $this = $(this);
        var id = $this.data('id');
        var type = $this.data('type');
        $.post('/api/useless', {
            'id': id,
            'type': type
        }, function (result) {
            if (result.status == "success") {
                if ($this.find('.amount').length == 0) {
                    $this.append('<span class="qa-action__link-num amount">0</span>');
                }
                $this.find('.amount').text(result.data.amount);
                // sweetAlert('success', result.data.message, 'success');
            } else {
                if (result.errorCode == 706) {
                    window.location.replace("/users/login");
                } else {
                    // sweetAlert('failed', result.errorMsg, 'error');
                }
            }
        });
    });

    $(document).on('click', '.best_answer_btn', function () {
        var $this = $(this);
        var id = $this.data('id');
        var type = $this.data('type');
        var answer_id = $this.data('answer_id');
        sweetAlert({
            title: '最佳解答',
            text: '確定要選為最佳解答嗎？',
            type: 'warning',
            buttons: true,
            buttons: ["取消", "確定"],
            dangerMode: true
        }).then(function (isConfirm) {
            if (!!isConfirm) {
                $.post('/api/answers/best', {
                    'id': id,
                    'type': type,
                    'answer_id': answer_id
                }, function (result) {
                    if (result.status == "success") {
                        window.location.reload();
                    }
                });
            } else {
                sweetAlert.close();
            }
        });
    });

    $('#tags').select2({
        tags: true,
        multiple: true,
        ajax: {
            url: '/api/tags/autocomplete',
            dataType: 'json',
            delay: 250,
            data: function (params) {
                return {
                    term: params.term,
                };
            },
            processResults: function (data, params) {
                return {
                    results: $(data).map(function (index, text) {
                        return {
                            id: text,
                            text: text
                        }
                    }).get()
                };
            },
            cache: true
        }
    });

    $(document).on('click', '.blacklist_btn', function () {
        var $this = $(this);
        var id = $this.data('id');
        $this.prop('disabled', true);
        var isBlackText = !!$this.text().trim().match(/^解除/igm) ? '解除' : '';
        sweetAlert({
            title: "封鎖",
            text: "確定" + isBlackText + "封鎖？",
            type: "warning",
            buttons: true,
            buttons: ["取消", "確定" + isBlackText + "封鎖"],
            dangerMode: true
            // showCancelButton: true,
            // confirmButtonColor: "#DD6B55",
            // confirmButtonText: "確定" + isBlackText + "封鎖",
            // cancelButtonText: "取消",
            // closeOnConfirm: false,
            // closeOnCancel: false
        }).then(function (isConfirm) {
            if (!!isConfirm) {
                $.post('/api/blacklist', {
                    'id': id
                }, function (result) {
                    if (result.errorCode == 706) {
                        window.location.replace("/users/login");
                    }
                    if (result.data.messages == 'Created') {
                        $this.find('span').text('解除封鎖 ' + $this.data('nickname'));
                        sweetAlert('封鎖成功', '', 'success');
                    } else {
                        $this.find('span').text('封鎖 ' + $this.data('nickname'));
                        sweetAlert('解除封鎖成功', '', 'success');
                    }
                });
            } else {
                sweetAlert.close();
            }
            $this.prop('disabled', false);
        });
    });

    $(document).on('click', '.remove_collection_btn', function () {
        var $this = $(this);
        var id = $this.data('id');
        var type = $this.data('type');
        $.post('/api/remove_collection', {
            'id': id,
            'type': type
        }, function (result) {
            $this.find('i').toggleClass('fa-star-o fa-star');
        });
    });

    $(document).on('click', '.profile-side__title', function (event) {
        $(this).find('.profile-side__down .fa').toggleClass('fa-angle-down fa-angle-up');
        var text = $(this).next('.profile-side__list');
        text.slideToggle(300);
    });

    $(document).on('click', '.loadmore-comments', function (event) {
        $(this).parents('.comment').find('.comment__previous').slideToggle();
        $(this).find('span').toggleClass('active');
    });

    $(document).on('click', '.trainee__header', function (event) {
        $(this).find('.trainee__arrowBtn .fa').toggleClass('fa-caret-down fa-caret-up');
        var text = $(this).next('.trainee__body');
        text.slideToggle(300);
    });

    function searchToggle(status) {
        var searchBtn = $('#searchDropdown');
        var isToggle = (typeof status == 'undefined');
        var isActive = searchBtn.hasClass('menu__search-btn--active');
        var isOpen = isToggle ? !isActive : (status == 'open');
        searchBtn.toggleClass('menu__search-btn--active', isOpen);
        searchBtn.find('.menu__search-toggle').toggleClass('active', isOpen);
        searchBtn.parents('.menu').find('.menu__dropform').toggle(isOpen);
        $('.menu__mask').toggleClass('menu__mask--open', isOpen);
        $('body').css('margin-right', '');
        $('.menu--fixed').css('width', '');
        var width = $('body').width();
        $('body').toggleClass('mask__patch', isOpen);
        var scrollWidth = $('body').width() - width;
        if ($(window).height() < $(document).height() && isOpen) {
            $('body').css('margin-right', scrollWidth + 'px');
            $('.menu--fixed').css('width', 'calc(100% - ' + scrollWidth + 'px)');
        }
    }


    $('#searchDropdown').on('click', function (event) {
        searchToggle();
    });


    $(document).on('click', '.menu__mask', function (event) {
        searchToggle('close');
    });

    $('.menu__item.dropdown').on('shown.bs.dropdown', function () {
        searchToggle('close');
    })

    $(document).on('click', '.mk-instruction__btn', function (event) {
        $(this).parents('.mk-instruction').toggleClass('move');
        $(this).find('.fa').toggleClass('fa-caret-up fa-caret-down');
    });

    $(document).on('click', '.btn.btn-draft.save-group__btn', function (e) {
        var $this = $(this);
        var $form = $this.parents('form');
        var link = $form.attr('action');
        var $textarea = $form.find('textarea[name="description"]');
        var simplemde = $textarea.data('simplemde');
        var markdown_text = simplemde.value();
        $textarea.val(markdown_text);
        var param = $form.serialize();
        $this.val('儲存中...').prop('disabled', true);
        $.post(link, param).then(function (result, status) {
            if (status === 'success') {
                sweetAlert({
                    title: 'Tip',
                    text: '儲存成功',
                    icon: 'success',
                    timer: 1500
                });
            } else {
                sweetAlert({
                    title: 'Tip',
                    text: '儲存失敗',
                    icon: 'warning',
                    timer: 1500
                });
            }
        }).done(function () {
            $this.val('儲存草稿').prop('disabled', false);
            scrollToErrorMsg();
        });
        return false;
    });

    $(window).scroll(debounce(function () {
        var win_h = $(document).scrollTop();
        if (win_h >= $('.header').height()) {
            $('.menu').addClass('menu--fixed affix');
            // $('.navbar-brand').show();
        } else {
            $('.menu').removeClass('menu--fixed affix');
            // $('.navbar-brand').hide();
        }
    })).scroll();

    function debounce(func, wait, immediate) {
        var timeout;
        return function () {
            var context = this,
                args = arguments;
            var later = function () {
                timeout = null;
                if (!immediate) func.apply(context, args);
            };
            var callNow = immediate && !timeout;
            clearTimeout(timeout);
            timeout = setTimeout(later, wait);
            if (callNow) func.apply(context, args);
        };
    };

    $('[data-toggle="tooltip"]').tooltip();

    $('.loginMsg').click(function (event) {
        //
    });

    $(document).on('click', '.qa-action__link--reply', function (event) {
        var id = '#' + $(this).attr('href').split('#')[1];
        goScroll(id, -60);
        return false;
    });

    $('.mk-side a ').click(function () {
        var id = '#' + $(this).attr('href').split('#')[1];
        goScroll(id, 20);
        return false;
    });

    $("body").scrollspy({
        target: "#navbar-side",
        offset: 70
    })

    function goScroll(target, h) {
        var target_top = $(target).offset().top;
        var header_height = $('.navbar').height() - h;
        var sTop = target_top - header_height;
        $("html, body").stop().animate({
            scrollTop: sTop
        }, 500, function () {});
    }

    $('.comment__form, .reply__form, .talk__form').submit(function () {
        var $description = $(this).find('[name="description"]');
        var isNULL = '';
        if ($description.attr('id').split('_')[0] === 'SimpleMDE' || $description.hasClass('SimpleMDE')) {
            isNULL = !$description.data('simplemde').value();
        } else {
            isNULL = !$description.val();
        }
        if (isNULL) {
            sweetAlert({
                title: 'Tip',
                text: '請輸入內容再發表',
                type: 'warning',
                timer: 3000
            });
            return false;
        }
    });

    $(document).on('click', '.index-tab .tabs-item__link', function () {
        var $this = $(this);
        var group = $this.parents('.index-tab');
        var target_id = $this.attr('href');
        group.find('a').each(function (i, elm) {
            var $elm = $(elm);
            var hide_id = $elm.attr('href');
            $elm.toggleClass('tabs-item__link--active tabs-item__link--hover');
            $(hide_id).hide();
        });
        $(target_id).fadeIn();
        return false;
    });


    $(document).on('click', '.qa-status__link', function (event) {
        event.preventDefault();

        $('.qa-status__link').removeClass('qa-status__link--active');
        $(this).addClass('qa-status__link--active');

        var $ans = $('.ans').length > 0 ? $('.ans') : $('.qa-panel.response');
        var timeSort = [];
        var likeSort = [];
        var timeData = {};
        var likeData = {};
        var type = $(this).data('type');
        $.each($ans, function (i, elm) {
            var self = $(elm);
            var time = self.find('.ans-header__leveltime').find('a').attr('title');
            var timestamp = +new Date(time);
            timeSort.push(timestamp + '|' + i);
            timeData[timestamp + '|' + i] = self.html();

            var likeNum = +self.find('.likeGroup__num').text();
            likeSort.push(likeNum + '|' + i);
            likeData[likeNum + '|' + i] = self.html();
        });

        var outputHTML = [];
        if (type == 'old') {
            timeSort.sort(function (a, b) {
                return +a.split('|')[0] - +b.split('|')[0];
            })
            $.each(timeSort, function (i, timestamp) {
                var html = timeData[timestamp];
                $ans.eq(i).html(html);
            });
        } else if (type == 'new') {
            timeSort.sort(function (a, b) {
                return +b.split('|')[0] - +a.split('|')[0];
            });
            $.each(timeSort, function (i, timestamp) {
                var html = timeData[timestamp];
                $ans.eq(i).html(html);
            });
        } else {
            likeSort.sort(function (a, b) {
                return +b.split('|')[0] - +a.split('|')[0];
            });
            $.each(likeSort, function (i, likeNum) {
                var html = likeData[likeNum];
                $ans.eq(i).html(html);
            });
        }

    });

    $(document).on('click', '.qa-action__link--share', function (event) {
        event.preventDefault();
        $(this).find('.list-share').toggleClass('list-share--open');
    });

    $(document).on('click', '.menu__profile-dropdown-post', function (event) {
        //
        $(this).find('.fa').toggleClass('fa-angle-down fa-angle-up');
        $(this).next('.menu__profile-dropdown-ul').toggle();
        // return false;
        event.stopPropagation();
    });

    $(".post-type__dropdown-menu div").click(function () {
        var e = $(this).closest(".post-type");
        e.find(".post-type__select-word").text($(this).text());
        e.find('input').val($(this).data('value'));
    });

    // Editor add Emoticon
    $('body').on('click', '.emoticon', function () {
        var imgLink = $(this).attr('src');
        var imgMK = '![' + imgLink + '](' + imgLink + ')';
        var $BearManEmoticonList = $('#BearManEmoticonList');
        var simplemde = $BearManEmoticonList.data('simplemde');
        simplemde.codemirror.replaceSelection(imgMK);
        swal.close();
    });

    $('.menu__ironman--show button').click(function () {
        $('#group').modal('show');
    });

    // check_forbid
    $('.check_forbid').find(':submit').click(function (event) {
        event.preventDefault();
        var $this = $(this);
        var $form = $this.parents('form.check_forbid');
        var desc_val = $form.find('textarea').data('simplemde').value();
        var form_data = {};
        $form.serializeArray().map(function (x) {
            form_data[x.name] = x.value;
        });
        form_data.description = desc_val;
        if (form_data._method) {
            delete form_data._method;
        }
        $.post('/api/forbid', form_data).then(function (result) {
            if (!result.status) {
                sweetAlert({
                    title: 'Tip',
                    text: result.message,
                    type: 'warning',
                    timer: 3000
                });
            } else {
                $form.submit();
            }
        });
    });

    // scroll to error msg
    function scrollToErrorMsg() {
        var ErrorMsg = $('.help-block, .post-header-error');
        var hasErrorMsg = (ErrorMsg.length > 0);
        if (hasErrorMsg) {
            var target_top = $(ErrorMsg).offset().top;
            var header_height = $('.menu__container').height() + 100 /* fixed label & input Height */ ;
            var sTop = target_top - header_height;

            $('html, body').stop().animate({
                scrollTop: sTop
            }, 500);
        }
    }
    scrollToErrorMsg();
});