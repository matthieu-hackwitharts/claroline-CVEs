# Remote code execution via arbitrary file upload (version : 13.5.7)

Claroline Connect app presents a RCE vulnerability because of the possibility to upload an arbitrary php file. This vulnerability is present on many upload forms, so I've
personnally choosed the resource icon section.

The route **core/Controller/APINew/FileController.php** filters the upload image type by using the getMimeType() function from Symfony : 

```php
public function uploadImage(Request $request): JsonResponse
    {
        $files = $request->files->all();

        $objects = [];
        foreach ($files as $file) {
            if (0 !== strpos($file->getMimeType(), 'image')) {
                throw new InvalidDataException('Invalid image type.');
            }

            $object = $this->crud->create(PublicFile::class, [], ['file' => $file, Crud::THROW_EXCEPTION]);
            $objects[] = $this->serializer->serialize($object);
        }

        return new JsonResponse($objects);
    }
```
    
    
<br>
    
It is possible to trick this function by add some magic bytes like ```GIF8;``` which corresponds to the GIF image file type. The mime type ```image/gif``` 
should be also applied.

![burp poc](https://raw.githubusercontent.com/matthieu-hackwitharts/claroline-CVEs/main/rce/poc_rce_burp.PNG)

<br>

Then it is possible to get RCE by using the upload php shell :

![rce poc](https://raw.githubusercontent.com/matthieu-hackwitharts/claroline-CVEs/main/rce/rce_new_poc.PNG)

**Fix suggestions :** Enhance file upload checks by adding real mime type verification (file content, bytes, size, etc). 


