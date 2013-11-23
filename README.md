yii-eav
=======

Installation
-------

1. Create EAV tables in your database with (can be found in eav.sql).
2. Add behavior and relation to your model.

        public function behaviors()
        {
            return array(
                ...
                'eav'=>array(
                    'class'=>'EavBehavior'
                )
                ...
            );
        }

        public function relations()
        {
            ...
            return array(
                'attributeValues' => array(self::HAS_MANY, 'EavAttributeValue', 'object_id', 'on' => 'attributeValues.object_entity="'.get_class($this).'"'),
            );
            ...
        }
        
3. Assign POST field while creating or updating the model. Be sure to save the object **before** setting values to EAV variables while creating.

            $client->save();
            ...
            $client->eavAttributes = $_POST['ClientAttribute'];
            $client->save();
