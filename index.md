---
title: Welcome to WardBalloon's Blog!
keywords: wardballoon, wardballoon blog, wardballoon website
tags:
  - introduction
sidebar: home_sidebar
permalink: index.html
summary: This is a welcome page for wardballoon's tech blog. This page explains blog concept and categories. The content in this page also contains the blog writer's information.
published: true
---

<html lang="en">
<head>
    {% include head.html %}
    <script>
        $(document).ready(function() {
            // Initialize navgoco with default options
            $("#mysidebar").navgoco({
                caretHtml: '',
                accordion: true,
                openClass: 'active', // open
                save: false, // leave false or nav highlighting doesn't work right
                cookie: {
                    name: 'navgoco',
                    expires: false,
                    path: '/'
                },
                slide: {
                    duration: 400,
                    easing: 'swing'
                }
            });

            $("#collapseAll").click(function(e) {
                e.preventDefault();
                $("#mysidebar").navgoco('toggle', false);
            });

            $("#expandAll").click(function(e) {
                e.preventDefault();
                $("#mysidebar").navgoco('toggle', true);
            });

        });

    </script>
    <script>
        $(function () {
            $('[data-toggle="tooltip"]').tooltip()
        })
    </script>
    <script>
        $(document).ready(function() {
            $("#tg-sb-link").click(function() {
                $("#tg-sb-sidebar").toggle();
                $("#tg-sb-content").toggleClass('col-md-9');
                $("#tg-sb-content").toggleClass('col-md-12');
                $("#tg-sb-icon").toggleClass('fa-toggle-on');
                $("#tg-sb-icon").toggleClass('fa-toggle-off');
            });
        });
    </script>
    {% if page.datatable == true %}
    <!-- Include the standard DataTables bits -->
    <link rel="stylesheet" type="text/css" href="//cdn.datatables.net/1.10.13/css/jquery.dataTables.css">
    <script type="text/javascript" charset="utf8" src="//cdn.datatables.net/1.10.13/js/jquery.dataTables.js"></script>
    <!-- First, this walks through the tables that occur between ...-begin
         and ...-end and add the "datatable" class to them.
         Then it invokes DataTable's standard initializer
         Credit here: http://www.beardedhacker.com/blog/2015/08/28/add-class-attribute-to-markdown-table/
      -->
    <script>
      $(document).ready(function(){
          $('div.datatable-begin').nextUntil('div.datatable-end', 'table').addClass('display');
          $('table.display').DataTable( {
              paging: true,
              stateSave: true,
              searching: true
          });
       });
    </script>
    {% endif %}

    $("#tg-sb-sidebar").toggle();
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <script type="text/javascript" charset="utf8" src="//cdn.datatables.net/1.10.13/js/jquery.dataTables.js"></script>
      <script>  $(document).ready(function() {$("#tg-sb-sidebar").toggle();});</script>

      <link rel="stylesheet" href="css/main_style.css">
      <title>Giorgi Tsereteli</title>

</head>

<body>
    <div class="grid-2">
        <div class="section-1">
            <i class="fas fa-code fa-5x white"></i>
            <h2>FirstName LastName</h2>
            <p>City,Country.</p>
            <a href="#"><i class="fab fa-twitter"></i></a>
            <a href="#"><i class="fab fa-github"></i></a>
        </div>
        <div class="section-2">
            <h2>About</h2>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Perferendis quas sint et nihil iusto eius nostrum sit error, repellat optio quisquam! Magnam dolore iusto cumque. Nostrum error iste neque maiores.</p>
            <h2>Skills</h2>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis in maiores autem quidem obcaecati excepturi! Cupiditate eaque itaque magni voluptatibus neque nobis est dolor? Atque sunt minus ipsa asperiores. At.</p>
            <h2>Projects</h2>
            <a href="#">Project 1</a>
            <a href="#">Project 2</a>
            <a href="#">Project 3</a>
            <a href="#">Project 4</a>
            <a href="#">Project 5</a>
            <h2>Contact</h2>
            <p>myEmail@email.com</p>
        </div>
    </div>
</body>
</html>
