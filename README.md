CoshiMediaBundle
=============

MediaBundle - for Symfony 2

Provides
---------

This bundle provides a service and base entity class.
Events are dispached after each media manager service action.


Setup
------

1. Create your media bundle for example AcmeMediaBudle
2. In this bundle create Media entity which extends Coshi\MediaBundle\Entity\Media, add id column and mapping of your choice
3. Add CoshiMediaBundle configuration to your appliaction's config.yml see config reference. Note that you have to create media_path in your web_root and give them proper permissions
4. Add CoshiMediaBundle to your AppKernel.php
5. Update your database schema
6. Add desired entities which have attached media and implement interfaces Coshi\MediaBundle\Model\MediaInterface for desired entity 
7. Now you can use coshi_media.media_manager service to perform file upload as simple as 

        $this->get('coshi_media.media_manager')->create($uploadedFileObject);
        $this->getDoctrine()->getManager()->flush();

Configuration reference
----------------

        coshi_media:
            media_class: Acme\MediaBundle\Entity\Media #Your entity class
            uploader:
                www_root: web #name of directory on which httpd's document root points
                media_path: media # name of directory where to upload files - www_root relative

Twig Extension
--------------

This bunlde provides simple extension to render a path to media in Twig
    
       {{ coshi_media_url(media) }}

Where of course media is a instance of mapped media class 

Events
------

Bundle generates couple events they are defined in Coshi\MediaBundle\MediaEvents
Events occurs on create of medium, update and delete. 
This is the way to extend bundle functionality.
        
        MediaEvents::CREATE_MEDIA
        MediaEvents::UPDATE_MEDIA
        MediaEvents::DELETE_MEDIA