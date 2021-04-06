# modal_after_post
show modal with jquery ajax after post



you could use ajax and bootstrap modal, crate a general modal somewhere in your html page(I usually have it in my base.html so it will be included in all pages) then submit your from by using ajax then ajax will provide success or error function regarding the response will receive from server-side. put that message in the modal. an example is:

somewhere inside base.html
 '''html
 
 <!-- Info General modal -->
    <div id="general_modal" class="modal fade " >
      <div class="modal-dialog ">
        <div class="modal-content ">
          <div class="modal-header bg-info">
            <h6 class="modal-title">Info header</h6>
            <button type="button" class="close" data-dismiss="modal">&times;</button>
          </div>
          <div class="modal-body">
          <!-- Empty will be field by Js -->
          </div>
        </div>
      </div>
    </div>
    <!-- /info General modal -->
    
    
'''

js and ajax function

''' js
$("#your-form").on('submit',function(e){
    e.preventDefault();
var ajax_link = this.getAttribute("data-ajax-link");
var target = this.getAttribute("data-target");
var title = this.getAttribute("data-modal-title");
var size = this.getAttribute("data-modal-size");
var bg = this.getAttribute("data-modal-content-bg");
// $(target+" .modal-body").load(ajax_link);
$.ajax({
    url:ajax_link,
    type:'POST',
    // data: $("#your-form-feilds").serialize(),

    success: function (response){
        $(target+" .modal-body").html(response);
    },
    /*
    error:function (response){
        new PNotify({
            title: 'oops',
            text:' Unable to load',
            type: 'error'
        });
    }
   */
});

$(target+" .modal-content").addClass(bg);
$(target+" .modal-title").html(title);
$(target+" .modal-dialog").removeClass().addClass("modal-dialog");
$(target+" .modal-dialog").addClass(size);
});
'''

html form

''' html
<form action="." method="post" id="your-form" class="btn btn-info  modal-ajax-load"
                        data-ajax-link="url"
                        data-toggle="modal"
                        data-modal-title="tilte"
                        data-target="#general_modal">
                        
                        
   '''
