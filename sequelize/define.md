public define(modelName: String, attributes: Object, options: Object): Model
Define a new model, representing a table in the DB.

The table columns are defined by the object that is given as the second argument. Each key of the object represents a column

Params:
Name	Type	Attribute	Description
modelName	String		
The name of the model. The model will be stored in sequelize.models under this name

attributes	Object		
An object, where each attribute is a column of the table. See Model.init

options	Object	
optional
These options are merged with the default define options provided to the Sequelize constructor and passed to Model.init()

Return:
Model
Example:
sequelize.define('modelName', {
    columnA: {
        type: Sequelize.BOOLEAN,
        validate: {
          is: ["[a-z]",'i'],        // will only allow letters
          max: 23,                  // only allow values <= 23
          isIn: {
            args: [['en', 'zh']],
            msg: "Must be English or Chinese"
          }
        },
        field: 'column_a'
        // Other attributes here
    },
    columnB: Sequelize.STRING,
    columnC: 'MY VERY OWN COLUMN TYPE'
})

sequelize.models.modelName // The model will now be available in models under the name given to define
See:
Model.init for a more comprehensive specification of the `options` and `attributes` objects.
The manual section about defining models
DataTypes For a list of possible data types
