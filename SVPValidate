const SVPValidate = (geojson) => {

    let problematic_record = [];

    try {

        // Rule: features must exist
        if(!geojson.hasOwnProperty('features')) {
            throw "features property must exist!"
        }

        // Rule: features must not be empty
        if (geojson.features.length < 1 ) {
            throw "features property must contain at leat one element"
        }

        geojson.features.forEach(f => {

            // Geometry must exixt
            if (!f.geometry || f.geometry === '') {
                throw "Geomety is required"
            }

            const prop = f.properties;


            // Rule: place is required
            if (!prop.place || prop.place === '') {
                throw "place property is required"
            }

            // Rule. reconstr must be null, 1, or 2
            if (prop.reconstr !== null && prop.reconstr !== 0 && prop.reconstr !== 1 && prop.reconstr !== 2){
                problematic_record.push(f);
                throw `Invalid value for reconstr: ${prop.reconstr}. Valid values are null, 0, 1 or 2`;
            }

            // Rule. part nust be one of null, s, u, l, or d
            if (prop.part !== null && prop.part !== 's' && prop.part !== 'u' && prop.part !== 'l' && prop.part !== 'd'){
                problematic_record.push(f);
                throw `Invalid value for part: ${prop.part}. Valid values are null, s, u, l or d`;
            }

            // Rule: phase must be a number
            if (typeof prop.phase !== 'number' && prop.phase !== null) {
                problematic_record.push(f);
                throw `Invalid value for phase: ${prop.phase}. Only null or numbers are supported`;
            }

            // Rule: lost must be one of null, 0 or 1
            if (prop.lost !== null && prop.lost !== 0 && prop.lost !== 1){
                problematic_record.push(f);
                throw `Invalid value for lost: ${prop.lost}. Valid values are null, 0 or 1`;
            }

            // Rule: source is required
            if (!prop.source || prop.source === '') {
                problematic_record.push(f);
                throw "source property is required"
            }

            // Rule: subsource is required
            if (!prop.subsource || prop.subsource === '') {
                problematic_record.push(f);
                throw "subsource property is required"
            }

            // Rule: date is requires and should meet the pattern yyyy-mm-dd
            if (!prop.date || ! /[0-9]{4}-[0-9]{2}-[0-9]{2}/.test(prop.date)) {
                problematic_record.push(f);
                throw `Date is required, and should be formatted as yyyy-mm-dd. Invalid ${prop.date}`;
            }

        });

        return {
            status: 'success',
            text: 'Validation passed!'
        };

    } catch (error) {
        return {
            status: 'error',
            debug: problematic_record,
            text: `Error! Validation failed with message: ${error}`
        };
    }
};
