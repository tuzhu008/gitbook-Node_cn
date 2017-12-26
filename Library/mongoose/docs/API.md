- [index.js](#indexjs)
	- [Mongoose#Aggregate()](#mongooseaggregate)
	- [Mongoose#CastError(type, value, path, [reason])](#mongoosecasterrortype-value-path-reason)
	- [Mongoose#Collection()](#mongoosecollection)
	- [Mongoose#connect(uri(s), [options], [options.useMongoClient], [callback])](#mongooseconnecturis-options-optionsusemongoclient-callback)
	- [Mongoose#Connection()](#mongooseconnection)
	- [Mongoose#createConnection([uri], [options], [options.config], [options.config.autoIndex], [options.useMongoClient])](#mongoosecreateconnectionuri-options-optionsconfig-optionsconfigautoindex-optionsusemongoclient)
	- [Mongoose#disconnect([fn])](#mongoosedisconnectfn)
	- [Mongoose#Document()](#mongoosedocument)
	- [Mongoose#DocumentProvider()](#mongoosedocumentprovider)
	- [Mongoose#Error()](#mongooseerror)
	- [Mongoose#get(key)](#mongoosegetkey)
	- [Mongoose#getPromiseConstructor()](#mongoosegetpromiseconstructor)
	- [Mongoose#Model()](#mongoosemodel)
	- [Mongoose#modelNames()](#mongoosemodelnames)
	- [Mongoose()](#mongoose)
	- [Mongoose#Mongoose()](#mongoosemongoose)
	- [Mongoose#plugin(fn, [opts])](#mongoosepluginfn-opts)
	- [function Object() { [native code] }#Promise()](#function-object-native-code-promise)
	- [Mongoose#PromiseProvider()](#mongoosepromiseprovider)
	- [Mongoose#Query()](#mongoosequery)
	- [Mongoose#Schema()](#mongooseschema)
	- [Mongoose#SchemaType()](#mongooseschematype)
	- [Mongoose#set(key, value)](#mongoosesetkey-value)
	- [()](#)
	- [Mongoose#VirtualType()](#mongoosevirtualtype)
	- [Mongoose#connection](#mongooseconnection)
	- [Mongoose#mongo](#mongoosemongo)
	- [Mongoose#mquery](#mongoosemquery)
	- [Mongoose#SchemaTypes](#mongooseschematypes)
	- [Mongoose#Types](#mongoosetypes)
	- [Mongoose#version](#mongooseversion)
- [types/array.js](#typesarrayjs)
	- [MongooseArray#$shift()](#mongoosearrayshift)
	- [MongooseArray#remove()](#mongoosearrayremove)
	- [MongooseArray.$pop()](#mongoosearraypop)
	- [MongooseArray.addToSet([args...])](#mongoosearrayaddtosetargs)
	- [MongooseArray.indexOf(obj)](#mongoosearrayindexofobj)
	- [MongooseArray.inspect()](#mongoosearrayinspect)
	- [MongooseArray.nonAtomicPush([args...])](#mongoosearraynonatomicpushargs)
	- [MongooseArray.pop()](#mongoosearraypop)
	- [MongooseArray.pull([args...])](#mongoosearraypullargs)
	- [MongooseArray.push([args...])](#mongoosearraypushargs)
	- [MongooseArray.set()](#mongoosearrayset)
	- [MongooseArray.shift()](#mongoosearrayshift)
	- [MongooseArray.sort()](#mongoosearraysort)
	- [MongooseArray.splice()](#mongoosearraysplice)
	- [MongooseArray.toObject(options)](#mongoosearraytoobjectoptions)
	- [MongooseArray.unshift()](#mongoosearrayunshift)
- [types/subdocument.js](#typessubdocumentjs)
	- [Subdocument#ownerDocument()](#subdocumentownerdocument)
	- [Subdocument#parent()](#subdocumentparent)
	- [Subdocument#remove([options], [callback])](#subdocumentremoveoptions-callback)
- [types/embedded.js](#typesembeddedjs)
	- [EmbeddedDocument#inspect()](#embeddeddocumentinspect)
	- [EmbeddedDocument#invalidate(path, err)](#embeddeddocumentinvalidatepath-err)
	- [EmbeddedDocument#ownerDocument()](#embeddeddocumentownerdocument)
	- [EmbeddedDocument#parent()](#embeddeddocumentparent)
	- [EmbeddedDocument#parentArray()](#embeddeddocumentparentarray)
	- [EmbeddedDocument#remove([options], [fn])](#embeddeddocumentremoveoptions-fn)
	- [EmbeddedDocument.markModified(path)](#embeddeddocumentmarkmodifiedpath)
- [types/buffer.js](#typesbufferjs)
	- [MongooseBuffer.copy(target)](#mongoosebuffercopytarget)
	- [MongooseBuffer.equals(other)](#mongoosebufferequalsother)
	- [MongooseBuffer.subtype(subtype)](#mongoosebuffersubtypesubtype)
	- [MongooseBuffer.toBSON()](#mongoosebuffertobson)
	- [MongooseBuffer.toObject([subtype])](#mongoosebuffertoobjectsubtype)
	- [MongooseBuffer.write()](#mongoosebufferwrite)
- [types/objectid.js](#typesobjectidjs)
	- [ObjectId()](#objectid)
- [types/decimal128.js](#typesdecimal128js)
	- [exports()](#exports)
- [types/documentarray.js](#typesdocumentarrayjs)
	- [MongooseDocumentArray.create(obj)](#mongoosedocumentarraycreateobj)
	- [MongooseDocumentArray.id(id)](#mongoosedocumentarrayidid)
	- [MongooseDocumentArray.inspect()](#mongoosedocumentarrayinspect)
	- [MongooseDocumentArray.toObject([options])](#mongoosedocumentarraytoobjectoptions)
- [promise.js](#promisejs)
	- [Promise#addBack(listener)](#promiseaddbacklistener)
	- [Promise#addCallback(listener)](#promiseaddcallbacklistener)
	- [Promise#addErrback(listener)](#promiseadderrbacklistener)
	- [Promise#end()](#promiseend)
	- [Promise#on(event, listener)](#promiseonevent-listener)
	- [Promise(fn)](#promisefn)
	- [Promise#reject(reason)](#promiserejectreason)
	- [Promise#resolve([err], [val])](#promiseresolveerr-val)
	- [Promise#then(onFulFill, onReject)](#promisethenonfulfill-onreject)
	- [Promise.complete(args)](#promisecompleteargs)
	- [Promise.ES6(resolver)](#promisees6resolver)
	- [Promise.fulfill(args)](#promisefulfillargs)
- [virtualtype.js](#virtualtypejs)
	- [VirtualType()](#virtualtype)
	- [VirtualType#get(fn)](#virtualtypegetfn)
	- [VirtualType#set(fn)](#virtualtypesetfn)
	- [VirtualType#applyGetters(value, scope)](#virtualtypeapplygettersvalue-scope)
	- [VirtualType#applySetters(value, scope)](#virtualtypeapplysettersvalue-scope)
- [utils.js](#utilsjs)
	- [exports.pluralization](#exportspluralization)
	- [exports.uncountables](#exportsuncountables)
- [drivers/node-mongodb-native/collection.js](#driversnode-mongodb-nativecollectionjs)
	- [function Object() { [native code] }#$format()](#function-object-native-code-format)
	- [function Object() { [native code] }#$print(](#function-object-native-code-print)
	- [NativeCollection#getIndexes(callback)](#nativecollectiongetindexescallback)
- [drivers/node-mongodb-native/connection.js](#driversnode-mongodb-nativeconnectionjs)
	- [NativeConnection#useDb(name)](#nativeconnectionusedbname)
	- [NativeConnection.STATES](#nativeconnectionstates)
- [browser.js](#browserjs)
	- [function Object() { [native code] }#Promise()](#function-object-native-code-promise)
	- [exports.Document()](#exportsdocument)
	- [exports.Error()](#exportserror)
	- [exports.PromiseProvider()](#exportspromiseprovider)
	- [exports.Schema()](#exportsschema)
	- [exports.VirtualType()](#exportsvirtualtype)
	- [exports#SchemaTypes](#exportsschematypes)
	- [exports#Types](#exportstypes)
- [ES6Promise.js](#es6promisejs)
	- [ES6Promise(fn)](#es6promisefn)
	- [schema.js](#schemajs)
	- [Schema#add(obj, prefix)](#schemaaddobj-prefix)
	- [Schema#clone()](#schemaclone)
	- [Schema#eachPath(fn)](#schemaeachpathfn)
	- [Schema#get(key)](#schemagetkey)
	- [Schema#index(fields, [options], [options.expires=null])](#schemaindexfields-options-optionsexpiresnull)
	- [Schema#indexes()](#schemaindexes)
	- [Schema#method(method, [fn])](#schemamethodmethod-fn)
	- [Schema#path(path, constructor)](#schemapathpath-constructor)
	- [Schema#pathType(path)](#schemapathtypepath)
	- [Schema#plugin(plugin, [opts])](#schemapluginplugin-opts)
	- [Schema#post(method, fn)](#schemapostmethod-fn)
	- [Schema#pre(method, callback)](#schemapremethod-callback)
	- [Schema#queue(name, args)](#schemaqueuename-args)
	- [Schema#remove(path)](#schemaremovepath)
	- [Schema#requiredPaths(invalidate)](#schemarequiredpathsinvalidate)
	- [Schema(definition, [options])](#schemadefinition-options)
	- [Schema#set(key, [value])](#schemasetkey-value)
	- [Schema#static(name, [fn])](#schemastaticname-fn)
	- [Schema#virtual(name, [options])](#schemavirtualname-options)
	- [Schema#virtualpath(name)](#schemavirtualpathname)
	- [Schema.indexTypes()](#schemaindextypes)
	- [Schema.reserved](#schemareserved)
	- [Schema.Types](#schematypes)
	- [Schema#childSchemas](#schemachildschemas)
	- [Schema#obj](#schemaobj)
- [document.js](#documentjs)
	- [MISSING method name](#missing-method-name)
	- [MISSING method name](#missing-method-name)
	- [Document#$ignore(path)](#documentignorepath)
	- [Document#$isDefault([path])](#documentisdefaultpath)
	- [Document#depopulate(path)](#documentdepopulatepath)
	- [Document#equals(doc)](#documentequalsdoc)
	- [Document#execPopulate()](#documentexecpopulate)
	- [Document#get(path, [type])](#documentgetpath-type)
	- [Document#init(doc, fn)](#documentinitdoc-fn)
	- [Document#inspect()](#documentinspect)
	- [Document#invalidate(path, errorMsg, value, [kind])](#documentinvalidatepath-errormsg-value-kind)
	- [Document#isDirectModified(path)](#documentisdirectmodifiedpath)
	- [Document#isDirectSelected(path)](#documentisdirectselectedpath)
	- [Document#isInit(path)](#documentisinitpath)
	- [Document#isModified([path])](#documentismodifiedpath)
	- [Document#isSelected(path)](#documentisselectedpath)
	- [Document#markModified(path, [scope])](#documentmarkmodifiedpath-scope)
	- [Document#modifiedPaths()](#documentmodifiedpaths)
	- [Document#populate([path], [callback])](#documentpopulatepath-callback)
	- [Document#populated(path)](#documentpopulatedpath)
	- [function Object() { [native code] }#save([options], [options.safe], [options.validateBeforeSave], [fn])](#function-object-native-code-saveoptions-optionssafe-optionsvalidatebeforesave-fn)
	- [(path, val, [type], [options])](#path-val-type-options)
	- [Document#toJSON(options)](#documenttojsonoptions)
	- [Document#toObject([options])](#documenttoobjectoptions)
	- [Document#toString()](#documenttostring)
	- [Document#unmarkModified(path)](#documentunmarkmodifiedpath)
	- [Document#update(doc, options, callback)](#documentupdatedoc-options-callback)
	- [Document#validate(optional, callback)](#documentvalidateoptional-callback)
	- [Document#validateSync(pathsToValidate)](#documentvalidatesyncpathstovalidate)
	- [Document.$markValid(path)](#documentmarkvalidpath)
	- [Document#errors](#documenterrors)
	- [Document#id](#documentid)
	- [Document#isNew](#documentisnew)
	- [Document#schema](#documentschema)
- [query.js](#queryjs)
	- [Query#$where(js)](#querywherejs)
	- [Query#all([path], val)](#queryallpath-val)
	- [Query#and(array)](#queryandarray)
	- [Query#batchSize(val)](#querybatchsizeval)
	- [Query#box(val, Upper)](#queryboxval-upper)
	- [Query#cast(model, [obj])](#querycastmodel-obj)
	- [Query#catch([reject])](#querycatchreject)
	- [Query#center()](#querycenter)
	- [Query#centerSphere([path], val)](#querycenterspherepath-val)
	- [Query#circle([path], area)](#querycirclepath-area)
	- [Query#collation(value)](#querycollationvalue)
	- [Query#comment(val)](#querycommentval)
	- [Query#count([criteria], [callback])](#querycountcriteria-callback)
	- [Query#cursor([options])](#querycursoroptions)
	- [Query#deleteMany([filter], [callback])](#querydeletemanyfilter-callback)
	- [Query#deleteOne([filter], [callback])](#querydeleteonefilter-callback)
	- [Query#distinct([field], [criteria], [callback])](#querydistinctfield-criteria-callback)
	- [Query#elemMatch(path, criteria)](#queryelemmatchpath-criteria)
	- [Query#equals(val)](#queryequalsval)
	- [Query#error(err)](#queryerrorerr)
	- [Query#exec([operation], [callback])](#queryexecoperation-callback)
	- [Query#exists([path], val)](#queryexistspath-val)
	- [Query#find([filter], [callback])](#queryfindfilter-callback)
	- [Query#findOne([filter], [projection], [options], [callback])](#queryfindonefilter-projection-options-callback)
	- [Query#findOneAndRemove([conditions], [options], [options.passRawResult], [options.strict], [callback])](#queryfindoneandremoveconditions-options-optionspassrawresult-optionsstrict-callback)
	- [Query#findOneAndUpdate([query], [doc], [options], [options.passRawResult], [options.strict], [options.multipleCastError], [callback])](#queryfindoneandupdatequery-doc-options-optionspassrawresult-optionsstrict-optionsmultiplecasterror-callback)
	- [Query#geometry(object)](#querygeometryobject)
	- [Query#getQuery()](#querygetquery)
	- [Query#getUpdate()](#querygetupdate)
	- [Query#gt([path], val)](#querygtpath-val)
	- [Query#gte([path], val)](#querygtepath-val)
	- [Query#hint(val)](#queryhintval)
	- [Query#in([path], val)](#queryinpath-val)
	- [Query#intersects([arg])](#queryintersectsarg)
	- [Query#lean(bool)](#queryleanbool)
	- [Query#limit(val)](#querylimitval)
	- [Query#lt([path], val)](#queryltpath-val)
	- [Query#lte([path], val)](#queryltepath-val)
	- [Query#maxDistance([path], val)](#querymaxdistancepath-val)
	- [Query#maxscan()](#querymaxscan)
	- [Query#maxScan(val)]()](#querymaxscanval)
	- [Query#merge(source)](#querymergesource)
	- [Query#merge(source)](#querymergesource)
	- [Query#mod([path], val)](#querymodpath-val)
	- [Query#mongooseOptions(options)](#querymongooseoptionsoptions)
	- [Query#ne([path], val)](#querynepath-val)
	- [Query#near([path], val)](#querynearpath-val)
	- [Query#nin([path], val)](#queryninpath-val)
	- [Query#nor(array)](#querynorarray)
	- [Query#or(array)](#queryorarray)
	- [Query#polygon([path], [coordinatePairs...])](#querypolygonpath-coordinatepairs)
	- [Query#populate(path, [select], [model], [match], [options])](#querypopulatepath-select-model-match-options)
	- [Query#read(pref, [tags])](#queryreadpref-tags)
	- [Query#regex([path], val)](#queryregexpath-val)
	- [Query#remove([filter], [callback])](#queryremovefilter-callback)
	- [Query#replaceOne([criteria], [doc], [options], [callback])](#queryreplaceonecriteria-doc-options-callback)
	- [Query#select(arg)](#queryselectarg)
	- [Query#selected()](#queryselected)
	- [Query#selectedExclusively()](#queryselectedexclusively)
	- [Query#selectedInclusively()](#queryselectedinclusively)
	- [Query#setOptions(options)](#querysetoptionsoptions)
	- [Query#size([path], val)](#querysizepath-val)
	- [Query#skip(val)](#queryskipval)
	- [Query#slaveOk(v)](#queryslaveokv)
	- [Query#slice([path], val)](#queryslicepath-val)
	- [Query#slice([path], [val])](#queryslicepath-val)
	- [Query#snapshot()](#querysnapshot)
	- [Query#sort(arg)](#querysortarg)
	- [Query#stream([options])](#querystreamoptions)
	- [Query#tailable(bool, [opts], [opts.numberOfRetries], [opts.tailableRetryInterval])](#querytailablebool-opts-optsnumberofretries-optstailableretryinterval)
	- [Query#then([resolve], [reject])](#querythenresolve-reject)
	- [Query#toConstructor()](#querytoconstructor)
	- [Query#update([criteria], [doc], [options], [options.multipleCastError], [callback])](#queryupdatecriteria-doc-options-optionsmultiplecasterror-callback)
	- [Query#updateMany([criteria], [doc], [options], [callback])](#queryupdatemanycriteria-doc-options-callback)
	- [Query#updateOne([criteria], [doc], [options], [callback])](#queryupdateonecriteria-doc-options-callback)
	- [Query#within()](#querywithin)
	- [Query#use$geoWithin](#queryusegeowithin)
- [aggregate.js](#aggregatejs)
	- [Aggregate#addCursorFlag(flag, value)](#aggregateaddcursorflagflag-value)
	- [Aggregate#addFields(arg)](#aggregateaddfieldsarg)
	- [Aggregate([ops])](#aggregateops)
	- [Aggregate#allowDiskUse(value, [tags])](#aggregateallowdiskusevalue-tags)
	- [Aggregate#append(ops)](#aggregateappendops)
	- [Aggregate#collation(collation, value)](#aggregatecollationcollation-value)
	- [Aggregate#cursor(options, options.batchSize, [options.useMongooseAggCursor])](#aggregatecursoroptions-optionsbatchsize-optionsusemongooseaggcursor)
	- [Aggregate#exec([callback])](#aggregateexeccallback)
	- [Aggregate#explain(callback)](#aggregateexplaincallback)
	- [Aggregate#facet(facet)](#aggregatefacetfacet)
	- [Aggregate#graphLookup(options)](#aggregategraphlookupoptions)
	- [Aggregate#group(arg)](#aggregategrouparg)
	- [Aggregate#limit(num)](#aggregatelimitnum)
	- [Aggregate#lookup(options)](#aggregatelookupoptions)
	- [Aggregate#match(arg)](#aggregatematcharg)
	- [Aggregate#model(model)](#aggregatemodelmodel)
	- [Aggregate#near(parameters)](#aggregatenearparameters)
	- [Aggregate#option(value)](#aggregateoptionvalue)
	- [Aggregate#pipeline()](#aggregatepipeline)
	- [Aggregate#project(arg)](#aggregateprojectarg)
	- [Aggregate#read(pref, [tags])](#aggregatereadpref-tags)
	- [Aggregate#sample(size)](#aggregatesamplesize)
	- [Aggregate#skip(num)](#aggregateskipnum)
	- [Aggregate#sort(arg)](#aggregatesortarg)
	- [Aggregate#then([resolve], [reject])](#aggregatethenresolve-reject)
	- [Aggregate#unwind(fields)](#aggregateunwindfields)
- [querystream.js](#querystreamjs)
	- [QueryStream#destroy([err])](#querystreamdestroyerr)
	- [QueryStream#pause()](#querystreampause)
	- [QueryStream#pipe()](#querystreampipe)
	- [QueryStream(query, [options])](#querystreamquery-options)
	- [QueryStream#resume()](#querystreamresume)
	- [QueryStream#paused](#querystreampaused)
	- [QueryStream#readable](#querystreamreadable)
- [services/cursor/eachAsync.js](#servicescursoreachasyncjs)
	- [module.exports(next, fn, options, [callback])](#moduleexportsnext-fn-options-callback)
- [error/index.js](#errorindexjs)
	- [MongooseError(msg)](#mongooseerrormsg)
	- [MongooseError.DocumentNotFoundError](#mongooseerrordocumentnotfounderror)
	- [MongooseError.messages](#mongooseerrormessages)
- [error/messages.js](#errormessagesjs)
	- [MongooseError.messages()](#mongooseerrormessages)
- [error/validation.js](#errorvalidationjs)
	- [ValidationError#toString()](#validationerrortostring)
- [model.js](#modeljs)
	- [Model#$where(argument)](#modelwhereargument)
	- [Model#increment()](#modelincrement)
	- [Model#model(name)](#modelmodelname)
	- [Model(doc)](#modeldoc)
	- [Model#remove([fn])](#modelremovefn)
	- [Model#save([options], [options.safe], [options.validateBeforeSave], [fn])](#modelsaveoptions-optionssafe-optionsvalidatebeforesave-fn)
	- [Model.aggregate([...], [callback])](#modelaggregate-callback)
	- [Model.count(conditions, [callback])](#modelcountconditions-callback)
	- [Model.create(doc(s), [callback])](#modelcreatedocs-callback)
	- [Model.createIndexes([options], [cb])](#modelcreateindexesoptions-cb)
	- [Model.deleteMany(conditions, [callback])](#modeldeletemanyconditions-callback)
	- [Model.deleteOne(conditions, [callback])](#modeldeleteoneconditions-callback)
	- [Model.discriminator(name, schema)](#modeldiscriminatorname-schema)
	- [Model.distinct(field, [conditions], [callback])](#modeldistinctfield-conditions-callback)
	- [Model.ensureIndexes([options], [cb])](#modelensureindexesoptions-cb)
	- [Model.find(conditions, [projection], [options], [callback])](#modelfindconditions-projection-options-callback)
	- [Model.findById(id, [projection], [options], [callback])](#modelfindbyidid-projection-options-callback)
	- [Model.findByIdAndRemove(id, [options], [callback])](#modelfindbyidandremoveid-options-callback)
	- [Model.findByIdAndUpdate(id, [update], [options], [callback])](#modelfindbyidandupdateid-update-options-callback)
	- [Model.findOne([conditions], [projection], [options], [callback])](#modelfindoneconditions-projection-options-callback)
	- [Model.findOneAndRemove(conditions, [options], [callback])](#modelfindoneandremoveconditions-options-callback)
	- [Model.findOneAndUpdate([conditions], [update], [options], [callback])](#modelfindoneandupdateconditions-update-options-callback)
	- [Model.geoNear(GeoJSON, options, [callback])](#modelgeoneargeojson-options-callback)
	- [Model.geoSearch(conditions, options, [callback])](#modelgeosearchconditions-options-callback)
	- [Model.hydrate(obj)](#modelhydrateobj)
	- [Model.init([callback])](#modelinitcallback)
	- [Model.insertMany(doc(s), [options], [options.ordered, [options.rawResult, [callback])](#modelinsertmanydocs-options-optionsordered-optionsrawresult-callback)
	- [Model.mapReduce(o, [callback])](#modelmapreduceo-callback)
	- [Model.populate(docs, options, [callback(err,doc)])](#modelpopulatedocs-options-callbackerrdoc)
	- [Model.remove(conditions, [callback])](#modelremoveconditions-callback)
	- [Model.replaceOne(conditions, doc, [options], [callback])](#modelreplaceoneconditions-doc-options-callback)
	- [Model.translateAliases(raw)](#modeltranslatealiasesraw)
	- [Model.update(conditions, doc, [options], [callback])](#modelupdateconditions-doc-options-callback)
	- [Model.updateMany(conditions, doc, [options], [callback])](#modelupdatemanyconditions-doc-options-callback)
	- [Model.updateOne(conditions, doc, [options], [callback])](#modelupdateoneconditions-doc-options-callback)
	- [Model.where(path, [val])](#modelwherepath-val)
	- [Model#$where](#modelwhere)
	- [Model#base](#modelbase)
	- [Model#baseModelName](#modelbasemodelname)
	- [Model#collection](#modelcollection)
	- [Model#db](#modeldb)
	- [Model#discriminators](#modeldiscriminators)
	- [Model#modelName](#modelmodelname)
	- [Model#schema](#modelschema)
- [schema/array.js](#schemaarrayjs)
	- [SchemaArray#checkRequired(value)](#schemaarraycheckrequiredvalue)
	- [SchemaArray(key, cast, options)](#schemaarraykey-cast-options)
	- [SchemaArray.schemaName](#schemaarrayschemaname)
- [schema/boolean.js](#schemabooleanjs)
	- [SchemaBoolean#checkRequired(value)](#schemabooleancheckrequiredvalue)
	- [SchemaBoolean(path, options)](#schemabooleanpath-options)
	- [SchemaBoolean.schemaName](#schemabooleanschemaname)
- [schema/mixed.js](#schemamixedjs)
	- [Mixed(path, options)](#mixedpath-options)
	- [Mixed.schemaName](#mixedschemaname)
- [schema/embedded.js](#schemaembeddedjs)
	- [Embedded#discriminator(name, schema)](#embeddeddiscriminatorname-schema)
	- [Embedded(schema, key, options)](#embeddedschema-key-options)
- [schema/buffer.js](#schemabufferjs)
	- [SchemaBuffer#checkRequired(value, doc)](#schemabuffercheckrequiredvalue-doc)
	- [SchemaBuffer(key, options)](#schemabufferkey-options)
	- [SchemaBuffer#subtype(subtype)](#schemabuffersubtypesubtype)
	- [SchemaBuffer.schemaName](#schemabufferschemaname)
- [schema/objectid.js](#schemaobjectidjs)
	- [ObjectId#auto(turnOn)](#objectidautoturnon)
	- [ObjectId#checkRequired(value, doc)](#objectidcheckrequiredvalue-doc)
	- [ObjectId(key, options)](#objectidkey-options)
	- [ObjectId.schemaName](#objectidschemaname)
- [schema/string.js](#schemastringjs)
	- [SchemaString#checkRequired(value, doc)](#schemastringcheckrequiredvalue-doc)
	- [SchemaString#enum([args...])](#schemastringenumargs)
	- [SchemaString#lowercase()](#schemastringlowercase)
	- [SchemaString#match(regExp, [message])](#schemastringmatchregexp-message)
	- [SchemaString#maxlength(value, [message])](#schemastringmaxlengthvalue-message)
	- [SchemaString#minlength(value, [message])](#schemastringminlengthvalue-message)
	- [SchemaString(key, options)](#schemastringkey-options)
	- [SchemaString#trim()](#schemastringtrim)
	- [SchemaString#uppercase()](#schemastringuppercase)
	- [SchemaString.schemaName](#schemastringschemaname)
- [schema/decimal128.js](#schemadecimal128js)
	- [Decimal128#checkRequired(value, doc)](#decimal128checkrequiredvalue-doc)
	- [Decimal128(key, options)](#decimal128key-options)
	- [Decimal128.schemaName](#decimal128schemaname)
- [schema/documentarray.js](#schemadocumentarrayjs)
	- [DocumentArray(key, schema, options)](#documentarraykey-schema-options)
	- [DocumentArray.schemaName](#documentarrayschemaname)
- [schema/date.js](#schemadatejs)
	- [SchemaDate#checkRequired(value, doc)](#schemadatecheckrequiredvalue-doc)
	- [SchemaDate#expires(when)](#schemadateexpireswhen)
	- [SchemaDate#max(maximum, [message])](#schemadatemaxmaximum-message)
	- [SchemaDate#min(value, [message])](#schemadateminvalue-message)
	- [SchemaDate(key, options)](#schemadatekey-options)
	- [SchemaDate.schemaName](#schemadateschemaname)
- [schema/number.js](#schemanumberjs)
	- [SchemaNumber#checkRequired(value, doc)](#schemanumbercheckrequiredvalue-doc)
	- [SchemaNumber#max(maximum, [message])](#schemanumbermaxmaximum-message)
	- [SchemaNumber#min(value, [message])](#schemanumberminvalue-message)
	- [SchemaNumber(key, options)](#schemanumberkey-options)
	- [SchemaNumber.schemaName](#schemanumberschemaname)
- [cursor/QueryCursor.js](#cursorquerycursorjs)
	- [QueryCursor#addCursorFlag(flag, value)](#querycursoraddcursorflagflag-value)
	- [QueryCursor#close(callback)](#querycursorclosecallback)
	- [QueryCursor#eachAsync(fn, [options], [options.parallel], [callback])](#querycursoreachasyncfn-options-optionsparallel-callback)
	- [QueryCursor#map(fn)](#querycursormapfn)
	- [QueryCursor#next(callback)](#querycursornextcallback)
	- [QueryCursor(query, options)](#querycursorquery-options)
- [cursor/AggregationCursor.js](#cursoraggregationcursorjs)
	- [AggregationCursor#addCursorFlag(flag, value)](#aggregationcursoraddcursorflagflag-value)
	- [AggregationCursor(agg, options)](#aggregationcursoragg-options)
	- [AggregationCursor#close(callback)](#aggregationcursorclosecallback)
	- [AggregationCursor#eachAsync(fn, [callback])](#aggregationcursoreachasyncfn-callback)
	- [AggregationCursor#map(fn)](#aggregationcursormapfn)
	- [AggregationCursor#next(callback)](#aggregationcursornextcallback)
- [schematype.js](#schematypejs)
	- [SchemaType#default(val)](#schematypedefaultval)
	- [SchemaType#get(fn)](#schematypegetfn)
	- [SchemaType#index(options)](#schematypeindexoptions)
	- [SchemaType#required(required, [options.isRequired], [options.ErrorConstructor], [message])](#schematyperequiredrequired-optionsisrequired-optionserrorconstructor-message)
	- [SchemaType(path, [options], [instance])](#schematypepath-options-instance)
	- [SchemaType#select(val)](#schematypeselectval)
	- [SchemaType#set(fn)](#schematypesetfn)
	- [SchemaType#sparse(bool)](#schematypesparsebool)
	- [SchemaType#text(bool)](#schematypetextbool)
	- [SchemaType#unique(bool)](#schematypeuniquebool)
	- [SchemaType#validate(obj, [errorMsg], [type])](#schematypevalidateobj-errormsg-type)
- [connection.js](#connectionjs)
	- [Connection#close([force], [callback])](#connectioncloseforce-callback)
	- [Connection#collection(name, [options])](#connectioncollectionname-options)
	- [Connection(base)](#connectionbase)
	- [(collection, [options], [callback])](#collection-options-callback)
	- [(collection, [callback])](#collection-callback)
	- [([callback])](#callback)
	- [Connection#model(name, [schema], [collection])](#connectionmodelname-schema-collection)
	- [Connection#modelNames()](#connectionmodelnames)
	- [(connection_string, [database], [port], [options], [callback])](#connectionstring-database-port-options-callback)
	- [(uris, [database], [options], [callback])](#uris-database-options-callback)
	- [Connection#collections](#connectioncollections)
	- [Connection#config](#connectionconfig)
	- [Connection#db](#connectiondb)
	- [Connection#readyState](#connectionreadystate)
- [collection.js](#collectionjs)
	- [Collection(name, conn, opts)](#collectionname-conn-opts)
	- [Collection#createIndex()](#collectioncreateindex)
	- [Collection#ensureIndex()](#collectionensureindex)
	- [Collection#find()](#collectionfind)
	- [Collection#findAndModify()](#collectionfindandmodify)
	- [Collection#findOne()](#collectionfindone)
	- [Collection#getIndexes()](#collectiongetindexes)
	- [Collection#insert()](#collectioninsert)
	- [Collection#mapReduce()](#collectionmapreduce)
	- [Collection#save()](#collectionsave)
	- [Collection#update()](#collectionupdate)
	- [Collection#collectionName](#collectioncollectionname)
	- [Collection#conn](#collectionconn)
	- [Collection#name](#collectionname)

# index.js

> 源码：[index.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/index.js)

## Mongoose#Aggregate()

Mongoose 的 Aggregate 构造函数

## Mongoose#CastError(type, value, path, [reason])

Mongoose 的 CastError 构造函数

##### 参数:

  * `type` 	&lt;[String][]&gt; The name of the type
  * `value` &lt;[Any][]&gt; The value that failed to cast
  * `path` &lt;[String][]&gt; The path a.b.c in the doc where this cast error occurred
  * `[reason]` &lt;[Error][]&gt; The original error that was thrown

## Mongoose#Collection()

Mongoose 的 Collection 构造函数

## Mongoose#connect(uri(s), [options], [options.useMongoClient], [callback])

打开默认的 mongoose 连接

##### 参数：

  * `uri(s)` &lt;[String][]&gt;
  * `[options]` &lt;[Object][]&gt;
  * `[options.useMongoClient]` &lt;[Boolean][]&gt; false by default, set to true to use new mongoose connection logic
  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * &lt;[MongooseThenable][]&gt; pseudo-promise wrapper around this

##### 参见：

  * [Mongoose#createConnection](#mongoose-createConnection)

如果提供了参数，它们也会被适当地代理到 [Connection#open]() 或者 [Connection#openSet]()。

*传递的选项优先于连接字符串中包含的选项。*

##### 示例：

```js
mongoose.connect('mongodb://user:pass@localhost:port/database');

// replica sets 副本集
var uri = 'mongodb://user:pass@localhost:port,anotherhost:port,yetanother:port/mydatabase';
mongoose.connect(uri);

// 使用选项
mongoose.connect(uri, options);

// 连接到多个 mongos
var uri = 'mongodb://hostA:27501,hostB:27501';
var opts = { mongos: true };
mongoose.connect(uri, opts);

// 可选的回调， 当初始化连接完成时被触发
var uri = 'mongodb://nonexistent.domain:27000';
mongoose.connect(uri, function(error) {
  // 如果 error 是真值，那初始化连接失败
})
```

<!--sec data-title="源码" data-id="Mongoose_connect" data-show=true data-collapse=true ces-->
  ```js
  Mongoose.prototype.connect = function() {
    var conn = this.connection;
    if ((arguments.length === 2 || arguments.length === 3) &&
        typeof arguments[0] === 'string' &&
        typeof arguments[1] === 'object' &&
        arguments[1].useMongoClient === true) {
      return conn.openUri(arguments[0], arguments[1], arguments[2]);
    }
    if (rgxReplSet.test(arguments[0]) || checkReplicaSetInUri(arguments[0])) {
      return new MongooseThenable(this, conn.openSet.apply(conn, arguments));
    }

    return new MongooseThenable(this, conn.open.apply(conn, arguments));
  };
  Mongoose.prototype.connect.$hasSideEffects = true;
  ```
<!--endsec-->


## Mongoose#Connection()

Mongoose 的 [Connection](#connectionbase) 构造函数


## Mongoose#createConnection([uri], [options], [options.config], [options.config.autoIndex], [options.useMongoClient]) {#mongoose-createConnection}

创建一个 Connection 实例。

##### 参数：

  * `[uri]` &lt;[String][]&gt; a mongodb:// URI
  * `[options]` &lt;[Object][]&gt; options to pass to the driver
  * `[options.config]` &lt;[Object][]&gt; mongoose-specific options
  * `[options.config.autoIndex]` &lt;[Boolean][]&gt; set to false to disable automatic index creation for all models associated with this connection.
  * `[options.useMongoClient]` &lt;[Boolean][]&gt; false by default, set to true to use new mongoose connection logic

##### 返回值：

  * &lt;[Connection](#connectionbase), [Promise](#promisefn)&gt; the created Connection object, or promise that resolves to the connection if `useMongoClient` option specified.

##### 参见：

  * [Connection#open]()
  * [Connection#openSet]()

Each connection instance maps to a single database. This method is helpful when mangaging multiple db connections.

If arguments are passed, they are proxied to either [Connection#open]() or [Connection#openSet]() appropriately. This means we can pass db, server, and replset options to the driver. Note that the safe option specified in your schema will overwrite the safe db option specified here unless you set your schemas safe option to undefined. See [this](/Library/mongoose/docs/guide.md#safe) for more information.

*Options passed take precedence over options included in connection strings.*


##### 示例：

```js
// with mongodb:// URI
db = mongoose.createConnection('mongodb://user:pass@localhost:port/database');

// and options
var opts = { db: { native_parser: true }}
db = mongoose.createConnection('mongodb://user:pass@localhost:port/database', opts);

// replica sets
db = mongoose.createConnection('mongodb://user:pass@localhost:port,anotherhost:port,yetanother:port/database');

// and options
var opts = { replset: { strategy: 'ping', rs_name: 'testSet' }}
db = mongoose.createConnection('mongodb://user:pass@localhost:port,anotherhost:port,yetanother:port/database', opts);

// with [host, database_name[, port] signature
db = mongoose.createConnection('localhost', 'database', port)

// and options
var opts = { server: { auto_reconnect: false }, user: 'username', pass: 'mypassword' }
db = mongoose.createConnection('localhost', 'database', port, opts)

// initialize now, connect later
db = mongoose.createConnection();
db.open('localhost', 'database', port, [opts]);
```

<!--sec data-title="源码" data-id="Mongoose_createConnection" data-show=true data-collapse=true ces-->
  ```js
  Mongoose.prototype.createConnection = function(uri, options) {
    var conn = new Connection(this);
    this.connections.push(conn);

    var rsOption = options && (options.replset || options.replSet);

    if (options && options.useMongoClient) {
      return conn.openUri(uri, options);
    }

    if (arguments.length) {
      if (rgxReplSet.test(arguments[0]) || checkReplicaSetInUri(arguments[0])) {
        conn._openSetWithoutPromise.apply(conn, arguments);
      } else if (rsOption &&
          (rsOption.replicaSet || rsOption.rs_name)) {
        conn._openSetWithoutPromise.apply(conn, arguments);
      } else {
        conn._openWithoutPromise.apply(conn, arguments);
      }
    }

    return conn;
  };
  Mongoose.prototype.createConnection.$hasSideEffects = true;
  ```
<!--endsec-->

## Mongoose#disconnect([fn])

断开所有连接。

##### 参数：

  * `[fn]` &lt;[Function][]&gt; called after all connection close.

##### 返回值：

  * <MongooseThenable> pseudo-promise wrapper around this

<!--sec data-title="源码" data-id="Mongoose_disconnect" data-show=true data-collapse=true ces-->
  ```js
  Mongoose.prototype.disconnect = function(fn) {
    var _this = this;

    var Promise = PromiseProvider.get();
    return new MongooseThenable(this, new Promise.ES6(function(resolve, reject) {
      var remaining = _this.connections.length;
      if (remaining <= 0) {
        fn && fn();
        resolve();
        return;
      }
      _this.connections.forEach(function(conn) {
        conn.close(function(error) {
          if (error) {
            fn && fn(error);
            reject(error);
            return;
          }
          if (!--remaining) {
            fn && fn();
            resolve();
          }
        });
      });
    }));
  };
  Mongoose.prototype.disconnect.$hasSideEffects = true;
  ```
<!--endsec-->

## Mongoose#Document()

Mongoose 的 [Document](#documentjs) 构造函数

## Mongoose#DocumentProvider()

Mongoose 的 DocumentProvider 构造函数

## Mongoose#Error()

[MongooseError](#mongooseerrormsg) 构造函数。

## Mongoose#get(key)

获取 mongoose 选项。

##### 参数：

  * `key` &lt;[String][]&gt;

##### 示例：

```js
mongoose.get('test') // returns the 'test' value
```

## Mongoose#getPromiseConstructor()

返回当前的 ES6 样式的 promise 构造函数。在 Mongoose 4.x 中，等价于 `mongoose.Promise.ES6`，但是一旦我们去掉了 `.ES6` 位，就会改变。


Mongoose#model(name, [schema], [collection], [skipInit])
Defines a model or retrieves it.

##### 参数：
  * name &lt;[String][], [Function][]&gt;model name or class extending Model
  * [schema] <Schema>
  * [collection] &lt;[String][]&gt; name (optional, inferred from model name)
  * [skipInit] &lt;[Boolean][]&gt; whether to skip initialization (defaults to false)

Models defined on the `mongoose` instance are available to all connection created by the same `mongoose` instance.

##### 示例：

```js
var mongoose = require('mongoose');

// define an Actor model with this mongoose instance
mongoose.model('Actor', new Schema({ name: String }));

// create a new connection
var conn = mongoose.createConnection(..);

// retrieve the Actor model
var Actor = conn.model('Actor');
```

When no `collection` argument is passed, Mongoose produces a collection name by passing the model `name` to the [utils.toCollectionName]() method. This method pluralizes the name. If you don't like this behavior, either pass a collection name or set your schemas collection name option.

##### 示例：

```js
var schema = new Schema({ name: String }, { collection: 'actor' });

// or

schema.set('collection', 'actor');

// or

var collectionName = 'actor'
var M = mongoose.model('Actor', schema, collectionName)
```

<!--sec data-title="源码" data-id="Mongoose_getPromiseConstructor" data-show=true data-collapse=true ces-->
```js
Mongoose.prototype.model = function(name, schema, collection, skipInit) {
  var model;
  if (typeof name === 'function') {
    model = name;
    name = model.name;
    if (!(model.prototype instanceof Model)) {
      throw new mongoose.Error('The provided class ' + name + ' must extend Model');
    }
  }

  if (typeof schema === 'string') {
    collection = schema;
    schema = false;
  }

  if (utils.isObject(schema) && !(schema.instanceOfSchema)) {
    schema = new Schema(schema);
  }
  if (schema && !schema.instanceOfSchema) {
    throw new Error('The 2nd parameter to `mongoose.model()` should be a ' +
      'schema or a POJO');
  }

  if (typeof collection === 'boolean') {
    skipInit = collection;
    collection = null;
  }

  // handle internal options from connection.model()
  var options;
  if (skipInit && utils.isObject(skipInit)) {
    options = skipInit;
    skipInit = true;
  } else {
    options = {};
  }

  // look up schema for the collection.
  if (!this.modelSchemas[name]) {
    if (schema) {
      // cache it so we only apply plugins once
      this.modelSchemas[name] = schema;
    } else {
      throw new mongoose.Error.MissingSchemaError(name);
    }
  }

  if (schema) {
    this._applyPlugins(schema);
  }

  var sub;

  // connection.model() may be passing a different schema for
  // an existing model name. in this case don't read from cache.
  if (this.models[name] && options.cache !== false) {
    if (schema && schema.instanceOfSchema && schema !== this.models[name].schema) {
      throw new mongoose.Error.OverwriteModelError(name);
    }

    if (collection) {
      // subclass current model with alternate collection
      model = this.models[name];
      schema = model.prototype.schema;
      sub = model.__subclass(this.connection, schema, collection);
      // do not cache the sub model
      return sub;
    }

    return this.models[name];
  }

  // ensure a schema exists
  if (!schema) {
    schema = this.modelSchemas[name];
    if (!schema) {
      throw new mongoose.Error.MissingSchemaError(name);
    }
  }

  // Apply relevant "global" options to the schema
  if (!('pluralization' in schema.options)) schema.options.pluralization = this.options.pluralization;


  if (!collection) {
    collection = schema.get('collection') || format(name, schema.options);
  }

  var connection = options.connection || this.connection;
  model = this.Model.compile(model || name, schema, collection, connection, this);

  if (!skipInit) {
    model.init();
  }

  if (options.cache === false) {
    return model;
  }

  this.models[name] = model;
  return this.models[name];
};
Mongoose.prototype.model.$hasSideEffects = true;
```
<!--endsec-->

## Mongoose#Model()

Mongoose [Model](#modeldoc) 构造函数。

## Mongoose#modelNames()

返回一个在 Mongoose 实例上创建的模型名称数组。

##### 返回值：

  * &lt;[Array][]&gt;

##### 注意：

不包括使用 `connection.model()` 创建的模型的名称。

<!--sec data-title="源码" data-id="Mongoose_modelNames" data-show=true data-collapse=true ces-->
```js
Mongoose.prototype.modelNames = function() {
  var names = Object.keys(this.models);
  return names;
};
Mongoose.prototype.modelNames.$hasSideEffects = true;
```
<!--endsec-->

## Mongoose()

Mongoose 构造函数。

`mongoose` 模块的导出对象（exports）是该类的一个实例。大多数应用程序只会使用这个实例。

<!--sec data-title="源码" data-id="Mongoose" data-show=true data-collapse=true ces-->
```js
function Mongoose() {
  this.connections = [];
  this.models = {};
  this.modelSchemas = {};
  // default global options
  this.options = {
    pluralization: true
  };
  var conn = this.createConnection(); // default connection
  conn.models = this.models;

  Object.defineProperty(this, 'plugins', {
    configurable: false,
    enumerable: true,
    writable: false,
    value: [
      [saveSubdocs, { deduplicate: true }],
      [validateBeforeSave, { deduplicate: true }],
      [shardingPlugin, { deduplicate: true }]
    ]
  });
}

```
<!--endsec-->

## Mongoose#Mongoose()

Mongoose 构造函数

mongoose 模块的导出对象（exports）是该类的一个实例。大多数应用程序只会使用这个实例。

##### 示例：

```js
  var mongoose = require('mongoose');
  var mongoose2 = new mongoose.Mongoose();
```

## Mongoose#plugin(fn, [opts])

声明一个在所有模式上执行的全局插件。

##### 参数：
  * `fn` &lt;[Function][]&gt; plugin callback
  * `[opts]` &lt;[Object][]&gt; optional options

##### 返回值：

  * <Mongoose> this

##### 参见：

  * [plugins](/Library/mongoose/docs/plugins.md)

等效于在创建的每个模式上调用 `.plugin(fn)`。

<!--sec data-title="源码" data-id="Mongoose_Mongoose" data-show=true data-collapse=true ces-->
```js
Mongoose.prototype.plugin = function(fn, opts) {
  this.plugins.push([fn, opts]);
  return this;
};
Mongoose.prototype.plugin.$hasSideEffects = true;
```
<!--endsec-->

## function Object() { [native code] }#Promise()

Mongoose [Promise](#promisefn) 构造函数。

## Mongoose#PromiseProvider()

mongoose promises 的储存层

## Mongoose#Query()

Mongoose [Query]() 构造函数。

## Mongoose#Schema()

Mongoose [Schema](#schemadefinition-options) 构造函数

##### 示例：

```js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;
var CatSchema = new Schema(..);
```

## Mongoose#SchemaType()

Mongoose [SchemaType]() 构造函数

## Mongoose#set(key, value)

设置 mongoose 的选项

##### 参数：

  * `key` &lt;[String][]&gt;
  * `value` <String, Function, Boolean>

##### 示例：

```js
mongoose.set('test', value) // 设置 'test' 选项为 `value`

mongoose.set('debug', true) // enable logging collection methods + arguments to the console

mongoose.set('debug', function(collectionName, methodName, arg1, arg2...) {}); // use custom function to log collection methods + arguments
```

<!--sec data-title="源码" data-id="Mongoose_set" data-show=true data-collapse=true ces-->
```js
Mongoose.prototype.set = function(key, value) {
  if (arguments.length === 1) {
    return this.options[key];
  }

  this.options[key] = value;
  return this;
};
Mongoose.prototype.set.$hasSideEffects = true;
```
<!--endsec-->
## ()

为用户空间（user-land）暴露连接状态

<!--sec data-title="源码" data-id="__" data-show=true data-collapse=true ces-->
```js
Mongoose.prototype.STATES = STATES;
```
<!--endsec-->

## Mongoose#VirtualType()

Mongoose [VirtualType]() 构造函数

## Mongoose#connection

mongoose 模块的默认连接。

##### 示例：

```js
var mongoose = require('mongoose');
mongoose.connect(...);
mongoose.connection.on('error', cb);
```

这是为使用 [`mongoose.model`]() 创建的每个模型所默认使用的连接。

<!--sec data-title="源码" data-id="Mongoose_connection" data-show=true data-collapse=true ces-->
```js
```
<!--endsec-->

##### 返回值：

  * <Connection>

## Mongoose#mongo

Mongoose 使用的[原生的 node-mongodb 驱动器](https://github.com/mongodb/node-mongodb-native)。

<!--sec data-title="源码" data-id="Mongoose_mongo" data-show=true data-collapse=true ces-->
```js
Mongoose.prototype.mongo = require('mongodb');
```
<!--endsec-->

## Mongoose#mquery

Mongoose 使用的 [mquery](https://github.com/aheckmann/mquery) 查询构建器。

<!--sec data-title="源码" data-id="Mongoose_mquery" data-show=true data-collapse=true ces-->
```js
Mongoose.prototype.mquery = require('mquery');
```
<!--endsec-->

## Mongoose#SchemaTypes

各种各样的 Mongoose SchemaTypes。

##### 注意：

*用于向后兼容的 `mongoose.Schema.Types` 的别名。*

<!--sec data-title="源码" data-id="Mongoose_SchemaTypes" data-show=true data-collapse=true ces-->
```js
Mongoose.prototype.SchemaTypes = Schema.Types;
```
<!--endsec-->

##### 参见：

  * [Schema.SchemaTypes]()

## Mongoose#Types

各种各样的 Mongoose Types.

##### 示例：

```js
var mongoose = require('mongoose');
var array = mongoose.Types.Array;
```

##### 类型：

  * [ObjectId]()
  * [Buffer]()
  * [SubDocument]()
  * [Array]()
  * [DocumentArray]()

使用这个暴露来对 `ObjectId` 类型进行访问，我们可以根据需要构造 `id`。

```js
var ObjectId = mongoose.Types.ObjectId;
var id1 = new ObjectId;
```

<!--sec data-title="源码" data-id="Mongoose_Types" data-show=true data-collapse=true ces-->
```js
Mongoose.prototype.Types = Types;
```
<!--endsec-->

## Mongoose#version

Mongoose 版本

<!--sec data-title="源码" data-id="Mongoose_version" data-show=true data-collapse=true ces-->
```js
Mongoose.prototype.version = pkg.version;
```
<!--endsec-->

# types/array.js

## MongooseArray#$shift()

在每一个文档 `save()` 的情况下，自动地 shift 这个数组最多一次。

##### 参见：

  * [mongodb](http://www.mongodb.org/display/DOCS/Updating/#Updating-%24pop)

##### 注意：

*Calling this mulitple times on an array before saving sends the same command as calling it once.This update is implemented using the MongoDB $pop method which enforces this restriction.*

```js
doc.array = [1,2,3];

 var shifted = doc.array.$shift();
 console.log(shifted); // 1
 console.log(doc.array); // [2,3]

 // no affect
 shifted = doc.array.$shift();
 console.log(doc.array); // [2,3]

 doc.save(function (err) {
   if (err) return handleError(err);

   // we saved, now $shift works again
   shifted = doc.array.$shift();
   console.log(shifted ); // 2
   console.log(doc.array); // [3]
 })
```

## MongooseArray#remove()

[pull]() 的别名。

##### 参见：

  * [MongooseArray#pull]()
  * [mongodb](http://www.mongodb.org/display/DOCS/Updating/#Updating-%24pull)

## MongooseArray.$pop()

在每一个文档 `save()` 的情况下，自动地 pop 这个数组最多一次。

##### 参见：

  * [mongodb](http://www.mongodb.org/display/DOCS/Updating/#Updating-%24pop)

##### 注意：

*Calling this mulitple times on an array before saving sends the same command as calling it once.This update is implemented using the MongoDB $pop method which enforces this restriction.*

```js
doc.array = [1,2,3];

 var popped = doc.array.$pop();
 console.log(popped); // 3
 console.log(doc.array); // [1,2]

 // no affect
 popped = doc.array.$pop();
 console.log(doc.array); // [1,2]

 doc.save(function (err) {
   if (err) return handleError(err);

   // we saved, now $pop works again
   popped = doc.array.$pop();
   console.log(popped); // 2
   console.log(doc.array); // [1]
 })
```

## MongooseArray.addToSet([args...])

如果不存在，则将值添加到数组中。

##### 参数：
  * [args...] <T>

##### 返回值：

  * &lt;[Array][]&gt; the values that were added

##### 示例：

```js
console.log(doc.array) // [2,3,4]
var added = doc.array.addToSet(4,5);
console.log(doc.array) // [2,3,4,5]
console.log(added)     // [5]
```

## MongooseArray.indexOf(obj)

Return the index of obj or -1 if not found.

##### 参数：

obj &lt;[Object][]&gt; the item to look for

##### 返回值：

  * <Number>

## MongooseArray.inspect()

Helper for console.log

## MongooseArray.nonAtomicPush([args...])

Pushes items to the array non-atomically.

##### 参数：

  * [args...] <T>

##### 注意：

*marks the entire array as modified, which if saved, will store it as a $set operation, potentially overwritting any changes that happen between when you retrieved the object and when you save it.*

## MongooseArray.pop()

Wraps Array#pop with proper change tracking.

##### 参见：

  * [MongooseArray#$pop]()

##### 注意：

*marks the entire array as modified which will pass the entire thing to $set potentially overwritting any changes that happen between when you retrieved the object and when you save it.*

## MongooseArray.pull([args...])

Pulls items from the array atomically. Equality is determined by casting
the provided value to an embedded document and comparing using

[the Document.equals() function]().

##### 参数：

  * [args...] <T>

##### 参见：

  * mongodb

##### 示例：

```js
doc.array.pull(ObjectId)
doc.array.pull({ _id: 'someId' })
doc.array.pull(36)
doc.array.pull('tag 1', 'tag 2')
```

To remove a document from a subdocument array we may pass an object with a matching _id.

```js
doc.subdocs.push({ _id: 4815162342 })
doc.subdocs.pull({ _id: 4815162342 }) // removed
```

Or we may passing the _id directly and let mongoose take care of it.

```js
doc.subdocs.push({ _id: 4815162342 })
doc.subdocs.pull(4815162342); // works
```

The first pull call will result in a atomic operation on the database, if pull is called repeatedly without saving the document, a $set operation is used on the complete array instead, overwriting possible changes that happened on the database in the meantime.

## MongooseArray.push([args...])

Wraps [`Array#push`](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/push) with proper change tracking.

##### 参数：

  * [args...] &lt;[Object][]&gt;

## MongooseArray.set()

Sets the casted val at index i and marks the array modified.

##### 返回值：

  * &lt;[Array][]&gt; this

##### 示例：

```js
// given documents based on the following
var Doc = mongoose.model('Doc', new Schema({ array: [Number] }));

var doc = new Doc({ array: [2,3,4] })

console.log(doc.array) // [2,3,4]

doc.array.set(1,"5");
console.log(doc.array); // [2,5,4] // properly cast to number
doc.save() // the change is saved

// VS not using array#set
doc.array[1] = "5";
console.log(doc.array); // [2,"5",4] // no casting
doc.save() // change is not saved
```

## MongooseArray.shift()

Wraps [`Array#shift`](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/unshift) with proper change tracking.

##### 示例：

```js
doc.array = [2,3];
var res = doc.array.shift();
console.log(res) // 2
console.log(doc.array) // [3]
```

##### 注意：

*marks the entire array as modified, which if saved, will store it as a $set operation, potentially overwritting any changes that happen between when you retrieved the object and when you save it.*

## MongooseArray.sort()

Wraps [`Array#sort`](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/sort) with proper change tracking.

##### 注意：

*marks the entire array as modified, which if saved, will store it as a $set operation, potentially overwritting any changes that happen between when you retrieved the object and when you save it.*

## MongooseArray.splice()

Wraps [`Array#splice`](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/splice) with proper change tracking and casting.

##### 注意：

*marks the entire array as modified, which if saved, will store it as a $set operation, potentially overwritting any changes that happen between when you retrieved the object and when you save it.*

## MongooseArray.toObject(options)

Returns a native js Array.

##### 参数：

  * options &lt;[Object][]&gt;

##### 返回值：

  * &lt;[Array][]&gt;

## MongooseArray.unshift()

Wraps [`Array#unshift`](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/unshift) with proper change tracking.

##### 注意：

*marks the entire array as modified, which if saved, will store it as a $set operation, potentially overwritting any changes that happen between when you retrieved the object and when you save it.*

# types/subdocument.js

> 源码：[types/subdocument.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/types/subdocument.js)

## Subdocument#ownerDocument()

Returns the top level document of this sub-document.

##### 返回值：

  * <Document>

<!--sec data-title="源码" data-id="Subdocument_ownerDocument" data-show=true data-collapse=true ces-->
```js
Subdocument.prototype.ownerDocument = function() {
  if (this.$__.ownerDocument) {
    return this.$__.ownerDocument;
  }

  var parent = this.$parent;
  if (!parent) {
    return this;
  }

  while (parent.$parent || parent.__parent) {
    parent = parent.$parent || parent.__parent;
  }
  this.$__.ownerDocument = parent;
  return this.$__.ownerDocument;
};
```
<!--endsec-->

## Subdocument#parent()

Returns this sub-documents parent document.

<!--sec data-title="源码" data-id="Subdocument_parent" data-show=true data-collapse=true ces-->
```js
Subdocument.prototype.parent = function() {
  return this.$parent;
};
```
<!--endsec-->

## Subdocument#remove([options], [callback])

Null-out this subdoc

##### 参数：

  * [options] &lt;[Object][]&gt;
  * [callback] &lt;[Function][]&gt; optional callback for compatibility with Document.prototype.remove

<!--sec data-title="源码" data-id="Subdocument_remove" data-show=true data-collapse=true ces-->
```js
Subdocument.prototype.remove = function(options, callback) {
  if (typeof options === 'function') {
    callback = options;
    options = null;
  }

  registerRemoveListener(this);

  // If removing entire doc, no need to remove subdoc
  if (!options || !options.noop) {
    this.$parent.set(this.$basePath, null);
  }

  if (typeof callback === 'function') {
    callback(null);
  }
};
```
<!--endsec-->

# types/embedded.js

> 源码：[types/embedded.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/types/embedded.js)

## EmbeddedDocument#inspect()

Helper for console.log

<!--sec data-title="源码" data-id="EmbeddedDocument_inspect" data-show=true data-collapse=true ces-->
```js
EmbeddedDocument.prototype.inspect = function() {
  return this.toObject({
    transform: false,
    retainKeyOrder: true,
    virtuals: false,
    flattenDecimals: false
  });
};
```
<!--endsec-->

## EmbeddedDocument#invalidate(path, err)

Marks a path as invalid, causing validation to fail.

##### 参数：

  * path &lt;[String][]&gt; the field to invalidate
  * err <String, Error> error which states the reason path was invalid

##### 返回值：

  * &lt;[Boolean][]&gt;


<!--sec data-title="源码" data-id="EmbeddedDocument_invalidate" data-show=true data-collapse=true ces-->
```js
EmbeddedDocument.prototype.invalidate = function(path, err, val, first) {
  if (!this.__parent) {
    Document.prototype.invalidate.call(this, path, err, val);
    if (err.$isValidatorError) {
      return true;
    }
    throw err;
  }

  var index = this.__index;
  if (typeof index !== 'undefined') {
    var parentPath = this.__parentArray._path;
    var fullPath = [parentPath, index, path].join('.');
    this.__parent.invalidate(fullPath, err, val);
  }

  if (first) {
    this.$__.validationError = this.ownerDocument().$__.validationError;
  }

  return true;
};
```
<!--endsec-->

## EmbeddedDocument#ownerDocument()

Returns the top level document of this sub-document.

##### 返回值：

  * <Document>

<!--sec data-title="源码" data-id="EmbeddedDocument_ownerDocument" data-show=true data-collapse=true ces-->
```js
EmbeddedDocument.prototype.ownerDocument = function() {
  if (this.$__.ownerDocument) {
    return this.$__.ownerDocument;
  }

  var parent = this.__parent;
  if (!parent) {
    return this;
  }

  while (parent.__parent || parent.$parent) {
    parent = parent.__parent || parent.$parent;
  }

  this.$__.ownerDocument = parent;
  return this.$__.ownerDocument;
};
```
<!--endsec-->

## EmbeddedDocument#parent()

Returns this sub-documents parent document.

<!--sec data-title="源码" data-id="EmbeddedDocument_parent" data-show=true data-collapse=true ces-->
```js
EmbeddedDocument.prototype.parent = function() {
  return this.__parent;
};
```
<!--endsec-->

## EmbeddedDocument#parentArray()

Returns this sub-documents parent array.

<!--sec data-title="源码" data-id="EmbeddedDocument_parentArray" data-show=true data-collapse=true ces-->
```js
EmbeddedDocument.prototype.parentArray = function() {
  return this.__parentArray;
};
```
<!--endsec-->

## EmbeddedDocument#remove([options], [fn])

Removes the subdocument from its parent array.

##### 参数：
  * [options] &lt;[Object][]&gt;
  * [fn] &lt;[Function][]&gt;

<!--sec data-title="源码" data-id="EmbeddedDocument_remove" data-show=true data-collapse=true ces-->
```js
EmbeddedDocument.prototype.remove = function(options, fn) {
  if ( typeof options === 'function' && !fn ) {
    fn = options;
    options = undefined;
  }
  if (!this.__parentArray || (options && options.noop)) {
    fn && fn(null);
    return this;
  }

  var _id;
  if (!this.willRemove) {
    _id = this._doc._id;
    if (!_id) {
      throw new Error('For your own good, Mongoose does not know ' +
          'how to remove an EmbeddedDocument that has no _id');
    }
    this.__parentArray.pull({_id: _id});
    this.willRemove = true;
    registerRemoveListener(this);
  }

  if (fn) {
    fn(null);
  }

  return this;
};
```
<!--endsec-->

## EmbeddedDocument.markModified(path)

Marks the embedded doc modified.

<!--sec data-title="源码" data-id="EmbeddedDocument_markModified" data-show=true data-collapse=true ces-->
```js
EmbeddedDocument.prototype.markModified = function(path) {
  this.$__.activePaths.modify(path);
  if (!this.__parentArray) {
    return;
  }

  if (this.isNew) {
    // Mark the WHOLE parent array as modified
    // if this is a new document (i.e., we are initializing
    // a document),
    this.__parentArray._markModified();
  } else {
    this.__parentArray._markModified(this, path);
  }
};
```
<!--endsec-->

##### 参数：

  * `path` &lt;[String][]&gt; the path which changed

##### 示例：

```js
var doc = blogpost.comments.id(hexstring);
doc.mixed.type = 'changed';
doc.markModified('mixed.type');
```

# types/buffer.js

> 源码：[types/buffer.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/types/buffer.js)


## MongooseBuffer.copy(target)

Copies the buffer.

##### 参数：

    * target <Buffer>

##### 返回值：

    * <Number> The number of bytes copied.

##### 注意：

*Buffer#copy does not mark target as modified so you must copy from a MongooseBuffer for it to work as expected. This is a work around since copy modifies the target, not this.* *

## MongooseBuffer.equals(other)

Determines if this buffer is equals to other buffer

##### 参数：

  * other <Buffer>

##### 返回值：

  * &lt;[Boolean][]&gt;

## MongooseBuffer.subtype(subtype)

Sets the subtype option and marks the buffer modified.

##### 参数：

  * `subtype` <Hex>

##### 参见：

  * http://bsonspec.org/#/specification

##### SubTypes:

var bson = require('bson')
bson.BSON_BINARY_SUBTYPE_DEFAULT
bson.BSON_BINARY_SUBTYPE_FUNCTION
bson.BSON_BINARY_SUBTYPE_BYTE_ARRAY
bson.BSON_BINARY_SUBTYPE_UUID
bson.BSON_BINARY_SUBTYPE_MD5
bson.BSON_BINARY_SUBTYPE_USER_DEFINED

doc.buffer.subtype(bson.BSON_BINARY_SUBTYPE_UUID);

## MongooseBuffer.toBSON()

Converts this buffer for storage in MongoDB, including subtype

##### 返回值：

  * <Binary>


## MongooseBuffer.toObject([subtype])

Converts this buffer to its Binary type representation.

##### 参数：

  * [subtype] <Hex>

##### 返回值：

  * <Binary>

##### 参见：

  * http://bsonspec.org/#/specification

##### SubTypes:

var bson = require('bson')
bson.BSON_BINARY_SUBTYPE_DEFAULT
bson.BSON_BINARY_SUBTYPE_FUNCTION
bson.BSON_BINARY_SUBTYPE_BYTE_ARRAY
bson.BSON_BINARY_SUBTYPE_UUID
bson.BSON_BINARY_SUBTYPE_MD5
bson.BSON_BINARY_SUBTYPE_USER_DEFINED

doc.buffer.toObject(bson.BSON_BINARY_SUBTYPE_USER_DEFINED);

## MongooseBuffer.write()

Writes the buffer.

----

# types/objectid.js

> 源码：[types/objectid.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/types/objectid.js)

## ObjectId()

ObjectId type constructor

##### 示例：

```js
var id = new mongoose.Types.ObjectId;
```

----

# types/decimal128.js

> 源码：[types/decimal128.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/types/decimal128.js)


## exports()

ObjectId type constructor

##### 示例：

```js
var id = new mongoose.Types.ObjectId;
```

# types/documentarray.js

> 源码：[types/documentarray.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/types/documentarray.js)

## MongooseDocumentArray.create(obj)

Creates a subdocument casted to this schema.

##### 参数：

  * obj &lt;[Object][]&gt; the value to cast to this arrays SubDocument schema

This is the same subdocument constructor used for casting.

## MongooseDocumentArray.id(id)

Searches array items for the first document with a matching _id.

##### 参数：

  * `id` <ObjectId, String, Number, Buffer>
##### 返回值：

  * <EmbeddedDocument, null> the subdocument or null if not found.

##### 示例：

```js
var embeddedDoc = m.array.id(some_id);
```

## MongooseDocumentArray.inspect()

Helper for console.log

## MongooseDocumentArray.toObject([options])

Returns a native js Array of plain js objects

##### 参数：

  * `[options]` &lt;[Object][]&gt; optional options to pass to each documents <code>toObject</code> method call during conversion

##### 返回值：

  * &lt;[Array][]&gt;

##### 注意：

*Each sub-document is converted to a plain object by calling its #toObject method.*

# promise.js

> 源码：[promise.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/promise.js)


## Promise#addBack(listener)

Adds a single function as a listener to both err and complete.

##### 参数：

  * `listener` &lt;[Function][]&gt;

##### 返回值：

  * <Promise> this


It will be executed with traditional node.js argument position when the promise is resolved.

```js
promise.addBack(function (err, args...) {
  if (err) return handleError(err);
  console.log('success');
})
```

[mpromise#onResolve](https://github.com/aheckmann/mpromise#onresolve) 的别名。

*Deprecated. Use onResolve instead.*

## Promise#addCallback(listener)

Adds a listener to the complete (success) event.

##### 参数：

  * listener &lt;[Function][]&gt;

##### 返回值：

  * <Promise> this


[mpromise#onFulfill](https://github.com/aheckmann/mpromise#onfulfill) 的别名。

*Deprecated. Use onFulfill instead.*

## Promise#addErrback(listener)

Adds a listener to the err (rejected) event.

##### 参数：

  * listener &lt;[Function][]&gt;

##### 返回值：

  * <Promise> this

  [mpromise#onReject](https://github.com/aheckmann/mpromise#onreject) 的别名。

*Deprecated. Use onReject instead.*

## Promise#catch(onReject)

ES6-style `.catch()` shorthand

##### 参数：

  * onReject &lt;[Function][]&gt;

##### 返回值：

  * <Promise>


## Promise#end()

Signifies that this promise was the last in a chain of then()s: if a handler passed to the call to then which produced this promise throws, the exception will go uncaught.

##### 参见：

  * [mpromise#end](https://github.com/aheckmann/mpromise#end)

##### 示例：

```js
var p = new Promise;
p.then(function(){ throw new Error('shucks') });
setTimeout(function () {
  p.fulfill();
  // error was caught and swallowed by the promise returned from
  // p.then(). we either have to always register handlers on
  // the returned promises or we can do the following...
}, 10);

// this time we use .end() which prevents catching thrown errors
var p = new Promise;
var p2 = p.then(function(){ throw new Error('shucks') }).end(); // &lt;--
setTimeout(function () {
  p.fulfill(); // throws "shucks"
}, 10);
```

## Promise#error(err)

Rejects this promise with err.

##### 参数：

  * err <Error, String>

##### 返回值：

  * <Promise> this

If the promise has already been fulfilled or rejected, not action is taken.

Differs from [#reject]() by first casting err to an Error if it is not instanceof Error.

<!--sec data-title="源码" data-id="Promise_error" data-show=true data-collapse=true ces-->
```js
Promise.prototype.error = function(err) {
  if (!(err instanceof Error)) {
    if (err instanceof Object) {
      err = util.inspect(err);
    }
    err = new Error(err);
  }
  return this.reject(err);
};
```
<!--endsec-->

## Promise#on(event, listener)

Adds listener to the event.

##### 参数：

  * `event` &lt;[String][]&gt;

  * `listener` &lt;[Function][]&gt;

##### 返回值：

  * <Promise> this

##### 参见：

  * [mpromise#on](https://github.com/aheckmann/mpromise#on)

If event is either the success or failure event and the event has already been emitted, thelistener is called immediately and passed the results of the original emitted event.

## Promise(fn)

Promise constructor.

##### 参数：

  * fn &lt;[Function][]&gt; a function which will be called when the promise is resolved that accepts fn(err, ...){} as signature


##### 继承：

  * [mpromise](https://github.com/aheckmann/mpromise)


##### 事件：

  * `err`: Emits when the promise is rejected

  * `complete`: Emits when the promise is fulfilled

Promises are returned from executed queries.示例：

```js
var query = Candy.find({ bar: true });
var promise = query.exec();
```

DEPRECATED. Mongoose 5.0 will use native promises by default (or bluebird,
if native promises are not present) but still
support plugging in your own ES6-compatible promises library. Mongoose 5.0
will **not**support mpromise.

<!--sec data-title="源码" data-id="Promise" data-show=true data-collapse=true ces-->
```js
function Promise(fn) {
  MPromise.call(this, fn);
}
```
<!--endsec-->

## Promise#reject(reason)

Rejects this promise with reason.

##### 参数：

  * reason <Object, String, Error>

##### 返回值：

  * <Promise> this

##### 参见：

  * [mpromise#reject](https://github.com/aheckmann/mpromise#reject)

If the promise has already been fulfilled or rejected, not action is taken.

## Promise#resolve([err], [val])

Resolves this promise to a rejected state if err is passed or a fulfilled state if no err is passed.

##### 参数：

  * [err] &lt;[Error][]&gt; error or null
  * [val] &lt;[Object][]&gt; value to fulfill the promise with

If the promise has already been fulfilled or rejected, not action is taken.

err will be cast to an Error if not already instanceof Error.

##### 注意：

*overrides mpromise#resolve to provide error casting.*

<!--sec data-title="源码" data-id="Promise_resolve" data-show=true data-collapse=true ces-->
```js
Promise.prototype.resolve = function(err) {
  if (err) return this.error(err);
  return this.fulfill.apply(this, Array.prototype.slice.call(arguments, 1));
};
```
<!--endsec-->

## Promise#then(onFulFill, onReject)

Creates a new promise and returns it. If onFulfill or onReject are passed, they are added as SUCCESS/ERROR callbacks to this promise after the nextTick.

##### 参数：

  * `onFulFill` &lt;[Function][]&gt;

  * `onReject` &lt;[Function][]&gt;

##### 返回值：

  * <Promise> newPromise

##### 参见：

  * [promises-A+](https://github.com/promises-aplus/promises-spec)
  * [mpromise#then](https://github.com/aheckmann/mpromise#then)


Conforms to promises/A+ specification.

##### 示例：

```js
var promise = Meetups.find({ tags: 'javascript' }).select('_id').exec();
promise.then(function (meetups) {
  var ids = meetups.map(function (m) {
    return m._id;
  });
  return People.find({ meetups: { $in: ids } }).exec();
}).then(function (people) {
  if (people.length &lt; 10000) {
    throw new Error('Too few people!!!');
  } else {
    throw new Error('Still need more people!!!');
  }
}).then(null, function (err) {
  assert.ok(err instanceof Error);
});
```

## Promise.complete(args)

Fulfills this promise with passed arguments.

##### 参数：

  * args <T>


[mpromise#fulfill](https://github.com/aheckmann/mpromise#fulfill) 的别名。

*Deprecated. Use fulfill instead.*

## Promise.ES6(resolver)

ES6-style promise constructor wrapper around mpromise.

<!--sec data-title="源码" data-id="Promise_ES6" data-show=true data-collapse=true ces-->
```js
Promise.ES6 = function(resolver) {
  var promise = new Promise();

  // No try/catch for backwards compatibility
  resolver(
    function() {
      promise.complete.apply(promise, arguments);
    },
    function(e) {
      promise.error(e);
    });

  return promise;
};
```
<!--endsec-->

##### 参数：

  * resolver &lt;[Function][]&gt;

##### 返回值：

  * <Promise> new promise

## Promise.fulfill(args)

Fulfills this promise with passed arguments.

##### 参数：

  * args <T>

##### 参见：

  * https://github.com/aheckmann/mpromise#fulfill

----

# virtualtype.js

> 源码：[virtualtype.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/virtualtype.js)


## VirtualType()

VirtualType constructor

This is what mongoose uses to define virtual attributes via Schema.prototype.virtual.

##### 示例：

```js
var fullname = schema.virtual('fullname');
fullname instanceof mongoose.VirtualType // true
```

<!--sec data-title="源码" data-id="VirtualType" data-show=true data-collapse=true ces-->
```js
function VirtualType(options, name) {
  this.path = name;
  this.getters = [];
  this.setters = [];
  this.options = options || {};
}
```
<!--endsec-->

## VirtualType#get(fn)

Defines a getter.

##### 参数：

  * fn &lt;[Function][]&gt;

##### 返回值：

  * <VirtualType> this

##### 示例：

```js
var virtual = schema.virtual('fullname');
virtual.get(function () {
  return this.name.first + ' ' + this.name.last;
});
```

<!--sec data-title="源码" data-id="VirtualType_get" data-show=true data-collapse=true ces-->
```js
VirtualType.prototype.get = function(fn) {
  this.getters.push(fn);
  return this;
};
```
<!--endsec-->

## VirtualType#set(fn)

Defines a setter.

##### 参数：

  * `fn` &lt;[Function][]&gt;

##### 返回值：

  * <VirtualType> this

##### 示例：

```js
var virtual = schema.virtual('fullname');
virtual.set(function (v) {
  var parts = v.split(' ');
  this.name.first = parts[0];
  this.name.last = parts[1];
});
```

<!--sec data-title="源码" data-id="VirtualType_set" data-show=true data-collapse=true ces-->
```js
VirtualType.prototype.set = function(fn) {
  this.setters.push(fn);
  return this;
};
```
<!--endsec-->

## VirtualType#applyGetters(value, scope)

Applies getters to value using optional scope.

##### 参数：

  * value &lt;[Object][]&gt;

  * scope &lt;[Object][]&gt;

##### 返回值：

  * <T> the value after applying all getters

<!--sec data-title="源码" data-id="VirtualType_applyGetters" data-show=true data-collapse=true ces-->
```js
VirtualType.prototype.applyGetters = function(value, scope) {
  var v = value;
  for (var l = this.getters.length - 1; l >= 0; l--) {
    v = this.getters[l].call(scope, v, this);
  }
  return v;
};
```
<!--endsec-->


## VirtualType#applySetters(value, scope)

Applies setters to value using optional scope.

##### 参数：

  * `value` &lt;[Object][]&gt;

  * `scope` &lt;[Object][]&gt;

##### 返回值：

  * <T> the value after applying all setters

<!--sec data-title="源码" data-id="VirtualType_applySetters" data-show=true data-collapse=true ces-->
```js
VirtualType.prototype.applySetters = function(value, scope) {
  var v = value;
  for (var l = this.setters.length - 1; l >= 0; l--) {
    v = this.setters[l].call(scope, v, this);
  }
  return v;
};
```
<!--endsec-->

----

# utils.js

> 源码：[utils.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/utils.js)


## exports.pluralization

Pluralization rules.

<!--sec data-title="源码" data-id="VirtualType_pluralization" data-show=true data-collapse=true ces-->
```js
exports.pluralization = [
  [/(m)an$/gi, '$1en'],
  [/(pe)rson$/gi, '$1ople'],
  [/(child)$/gi, '$1ren'],
  [/^(ox)$/gi, '$1en'],
  [/(ax|test)is$/gi, '$1es'],
  [/(octop|vir)us$/gi, '$1i'],
  [/(alias|status)$/gi, '$1es'],
  [/(bu)s$/gi, '$1ses'],
  [/(buffal|tomat|potat)o$/gi, '$1oes'],
  [/([ti])um$/gi, '$1a'],
  [/sis$/gi, 'ses'],
  [/(?:([^f])fe|([lr])f)$/gi, '$1$2ves'],
  [/(hive)$/gi, '$1s'],
  [/([^aeiouy]|qu)y$/gi, '$1ies'],
  [/(x|ch|ss|sh)$/gi, '$1es'],
  [/(matr|vert|ind)ix|ex$/gi, '$1ices'],
  [/([m|l])ouse$/gi, '$1ice'],
  [/(kn|w|l)ife$/gi, '$1ives'],
  [/(quiz)$/gi, '$1zes'],
  [/s$/gi, 's'],
  [/([^a-z])$/, '$1'],
  [/$/gi, 's']
];
var rules = exports.pluralization;
```
<!--endsec-->

These rules are applied while processing the argument to toCollectionName.

## exports.uncountables

Uncountable words.

<!--sec data-title="源码" data-id="exports_uncountables" data-show=true data-collapse=true ces-->
```js
exports.uncountables = [
  'advice',
  'energy',
  'excretion',
  'digestion',
  'cooperation',
  'health',
  'justice',
  'labour',
  'machinery',
  'equipment',
  'information',
  'pollution',
  'sewage',
  'paper',
  'money',
  'species',
  'series',
  'rain',
  'rice',
  'fish',
  'sheep',
  'moose',
  'deer',
  'news',
  'expertise',
  'status',
  'media'
];
var uncountables = exports.uncountables;
```
<!--endsec-->

These words are applied while processing the argument to toCollectionName.

----

# drivers/node-mongodb-native/collection.js

> 源码：[drivers/node-mongodb-native/collection.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/drivers/node-mongodb-native/collection.js)


## function Object() { [native code] }#$format()

Formatter for debug print args

## function Object() { [native code] }#$print(

Debug print helper

## NativeCollection#getIndexes(callback)

Retreives information about this collections indexes.

##### 参数：

  * `callback` &lt;[Function][]&gt;

----

# drivers/node-mongodb-native/connection.js

> 源码：[drivers/node-mongodb-native/connection.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/drivers/node-mongodb-native/connection.js)


## NativeConnection#useDb(name)


Switches to a different database using the same connection pool.

##### 参数：

  * `name` &lt;[String][]&gt; The database name

##### 返回值：

  * <Connection> New Connection Object

Returns a new connection object, with the new db.

<!--sec data-title="源码" data-id="NativeConnection_useDb" data-show=true data-collapse=true ces-->
```js
NativeConnection.prototype.useDb = function(name) {
  // we have to manually copy all of the attributes...
  var newConn = new this.constructor();
  newConn.name = name;
  newConn.base = this.base;
  newConn.collections = {};
  newConn.models = {};
  newConn.replica = this.replica;
  newConn.hosts = this.hosts;
  newConn.host = this.host;
  newConn.port = this.port;
  newConn.user = this.user;
  newConn.pass = this.pass;
  newConn.options = this.options;
  newConn._readyState = this._readyState;
  newConn._closeCalled = this._closeCalled;
  newConn._hasOpened = this._hasOpened;
  newConn._listening = false;

  // First, when we create another db object, we are not guaranteed to have a
  // db object to work with. So, in the case where we have a db object and it
  // is connected, we can just proceed with setting everything up. However, if
  // we do not have a db or the state is not connected, then we need to wait on
  // the 'open' event of the connection before doing the rest of the setup
  // the 'connected' event is the first time we'll have access to the db object

  var _this = this;

  if (this.db && this._readyState === STATES.connected) {
    wireup();
  } else {
    this.once('connected', wireup);
  }

  function wireup() {
    newConn.db = _this.db.db(name);
    newConn.onOpen();
    // setup the events appropriately
    listen(newConn);
  }

  newConn.name = name;

  // push onto the otherDbs stack, this is used when state changes
  this.otherDbs.push(newConn);
  newConn.otherDbs.push(this);

  return newConn;
};
```
<!--endsec-->

## NativeConnection.STATES

Expose the possible connection states.

<!--sec data-title="源码" data-id="NativeConnection_STATES" data-show=true data-collapse=true ces-->
```js
NativeConnection.STATES = STATES;
```
<!--endsec-->

----

# browser.js

> 源码：[browser.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/browser.js)


## function Object() { [native code] }#Promise()

The Mongoose [Promise] constructor.

## exports.Document()

The Mongoose browser [Document] constructor.

## exports.Error()

The MongooseError constructor.

## exports.PromiseProvider()

Storage layer for mongoose promises

## exports.Schema()

The Mongoose Schema constructor

##### 示例：

```js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;
var CatSchema = new Schema(..);
```

## exports.VirtualType()

The Mongoose VirtualType constructor

## exports#SchemaTypes

The various Mongoose SchemaTypes.

##### 注意：

*Alias of mongoose.Schema.Types for backwards compatibility.*

<!--sec data-title="源码" data-id="exports_SchemaTypes" data-show=true data-collapse=true ces-->
```js
exports.SchemaType = require('./schematype.js');
```
<!--endsec-->

##### 参见：

  * [Schema.SchemaTypes]()

## exports#Types

The various Mongoose Types.

##### 示例：

```js
var mongoose = require('mongoose');
var array = mongoose.Types.Array;
```

##### 类型：

  * [ObjectId]()
  * [Buffer]()
  * [SubDocument]()
  * [Array]()
  * [DocumentArray]()


Using this exposed access to the ObjectId type, we can construct ids on demand.

```js
var ObjectId = mongoose.Types.ObjectId;
var id1 = new ObjectId;
```

<!--sec data-title="源码" data-id="1" data-show=true data-collapse=true ces-->
```js
exports.Types = require('./types');
```
<!--endsec-->

----

# ES6Promise.js

> 源码：[ES6Promise.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/ES6Promise.js)


## ES6Promise(fn)

ES6 Promise wrapper constructor.

##### 参数：

  * `fn` &lt;[Function][]&gt; a function which will be called when the promise is resolved that accepts fn(err, ...){} as signature


Promises are returned from executed queries.

##### 示例：

```js
var query = Candy.find({ bar: true });
var promise = query.exec();
```

DEPRECATED. Mongoose 5.0 will use native promises by default (or bluebird,
if native promises are not present) but still
support plugging in your own ES6-compatible promises library. Mongoose 5.0
will **not** support mpromise.

<!--sec data-title="源码" data-id="2" data-show=true data-collapse=true ces-->
```js
function ES6Promise() {
  throw new Error('Can\'t use ES6 promise with mpromise style constructor');
}

ES6Promise.use = function(Promise) {
  ES6Promise.ES6 = Promise;
};

module.exports = ES6Promise;
```
<!--endsec-->

----


## schema.js

> 源码：[schema.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema.js)


## Schema#add(obj, prefix)

Adds key path / schema type pairs to this schema.

##### 参数：

  * obj &lt;[Object][]&gt;

  * prefix &lt;[String][]&gt;

##### 示例：

```js
var ToySchema = new Schema;
ToySchema.add({ name: 'string', color: 'string', price: 'number' });
```

<!--sec data-title="源码" data-id="3" data-show=true data-collapse=true ces-->
```js
Schema.prototype.add = function add(obj, prefix) {
  prefix = prefix || '';
  var keys = Object.keys(obj);

  for (var i = 0; i < keys.length; ++i) {
    var key = keys[i];

    if (obj[key] == null) {
      throw new TypeError('Invalid value for schema path `' + prefix + key + '`');
    }

    if (Array.isArray(obj[key]) && obj[key].length === 1 && obj[key][0] == null) {
      throw new TypeError('Invalid value for schema Array path `' + prefix + key + '`');
    }

    if (utils.isObject(obj[key]) &&
        (!obj[key].constructor || utils.getFunctionName(obj[key].constructor) === 'Object') &&
        (!obj[key][this.options.typeKey] || (this.options.typeKey === 'type' && obj[key].type.type))) {
      if (Object.keys(obj[key]).length) {
        // nested object { last: { name: String }}
        this.nested[prefix + key] = true;
        this.add(obj[key], prefix + key + '.');
      } else {
        if (prefix) {
          this.nested[prefix.substr(0, prefix.length - 1)] = true;
        }
        this.path(prefix + key, obj[key]); // mixed type
      }
    } else {
      if (prefix) {
        this.nested[prefix.substr(0, prefix.length - 1)] = true;
      }
      this.path(prefix + key, obj[key]);
    }
  }
};

```
<!--endsec-->

## Schema#clone()

Returns a deep copy of the schema

##### 返回值：

  * <Schema> the cloned schema


<!--sec data-title="源码" data-id="4" data-show=true data-collapse=true ces-->
```js
Schema.prototype.clone = function() {
  var s = new Schema(this.paths, this.options);
  // Clone the call queue
  var cloneOpts = { retainKeyOrder: true };
  s.callQueue = this.callQueue.map(function(f) { return f; });
  s.methods = utils.clone(this.methods, cloneOpts);
  s.statics = utils.clone(this.statics, cloneOpts);
  s.query = utils.clone(this.query, cloneOpts);
  s.plugins = Array.prototype.slice.call(this.plugins);
  s._indexes = utils.clone(this._indexes, cloneOpts);
  s.s.hooks = this.s.hooks.clone();
  return s;
};
```
<!--endsec-->


## Schema#eachPath(fn)

Iterates the schemas paths similar to Array#forEach.

##### 参数：

  * `fn` &lt;[Function][]&gt; callback function

##### 返回值：

  * <Schema> this
The callback is passed the pathname and schemaType as arguments on each iteration.

<!--sec data-title="源码" data-id="5" data-show=true data-collapse=true ces-->
```js
Schema.prototype.eachPath = function(fn) {
  var keys = Object.keys(this.paths),
      len = keys.length;

  for (var i = 0; i < len; ++i) {
    fn(keys[i], this.paths[keys[i]]);
  }

  return this;
};
```
<!--endsec-->


## Schema#get(key)

Gets a schema option.

##### 参数：

  * `key` &lt;[String][]&gt; option name


<!--sec data-title="源码" data-id="Schema_get" data-show=true data-collapse=true ces-->
```js
Schema.prototype.get = function(key) {
  return this.options[key];
};
```
<!--endsec-->

## Schema#index(fields, [options], [options.expires=null])

Defines an index (most likely compound) for this schema.

##### 参数：

  * fields &lt;[Object][]&gt;

  * [options] &lt;[Object][]&gt; Options to pass to MongoDB driver's createIndex() function

  * [options.expires=null] &lt;[String][]&gt; Mongoose-specific syntactic sugar, uses ms to convert expires option into seconds for the expireAfterSeconds in the above link.

##### 示例：

```js
schema.index({ first: 1, last: -1 })
```

<!--sec data-title="源码" data-id="Schema_index" data-show=true data-collapse=true ces-->
```js
Schema.prototype.index = function(fields, options) {
  options || (options = {});

  if (options.expires) {
    utils.expires(options);
  }

  this._indexes.push([fields, options]);
  return this;
};
```
<!--endsec-->

## Schema#indexes()

Compiles indexes from fields and schema-level indexes

<!--sec data-title="源码" data-id="Schema_indexes" data-show=true data-collapse=true ces-->
```js
```
<!--endsec-->
Schema#loadClass(model)
Loads an ES6 class into a schema. Maps setters + getters, static methods, and instance methods to schema virtuals, statics, and methods.

##### 参数：
model &lt;[Function][]&gt;
<!--sec data-title="源码" data-id="6" data-show=true data-collapse=true ces-->
```js
Schema.prototype.indexes = function() {
  'use strict';

  var indexes = [];
  var schemaStack = [];

  var collectIndexes = function(schema, prefix) {
    // Ignore infinitely nested schemas, if we've already seen this schema
    // along this path there must be a cycle
    if (schemaStack.indexOf(schema) !== -1) {
      return;
    }
    schemaStack.push(schema);

    prefix = prefix || '';
    var key, path, index, field, isObject, options, type;
    var keys = Object.keys(schema.paths);

    for (var i = 0; i < keys.length; ++i) {
      key = keys[i];
      path = schema.paths[key];

      if ((path instanceof MongooseTypes.DocumentArray) || path.$isSingleNested) {
        if (path.options.excludeIndexes !== true) {
          collectIndexes(path.schema, prefix + key + '.');
        }
      } else {
        index = path._index || (path.caster && path.caster._index);

        if (index !== false && index !== null && index !== undefined) {
          field = {};
          isObject = utils.isObject(index);
          options = isObject ? index : {};
          type = typeof index === 'string' ? index :
              isObject ? index.type :
                  false;

          if (type && ~Schema.indexTypes.indexOf(type)) {
            field[prefix + key] = type;
          } else if (options.text) {
            field[prefix + key] = 'text';
            delete options.text;
          } else {
            field[prefix + key] = 1;
          }

          delete options.type;
          if (!('background' in options)) {
            options.background = true;
          }

          indexes.push([field, options]);
        }
      }
    }

    schemaStack.pop();

    if (prefix) {
      fixSubIndexPaths(schema, prefix);
    } else {
      schema._indexes.forEach(function(index) {
        if (!('background' in index[1])) {
          index[1].background = true;
        }
      });
      indexes = indexes.concat(schema._indexes);
    }
  };

  collectIndexes(this);
  return indexes;
}
```
<!--endsec-->

## Schema#method(method, [fn])

Adds an instance method to documents constructed from Models compiled from this schema.

##### 参数：

  * method <String, Object> name

  * [fn] &lt;[Function][]&gt;


##### 示例：

```js
var schema = kittySchema = new Schema(..);

schema.method('meow', function () {
  console.log('meeeeeoooooooooooow');
})

var Kitty = mongoose.model('Kitty', schema);

var fizz = new Kitty;
fizz.meow(); // meeeeeooooooooooooow
```

If a hash of name/fn pairs is passed as the only argument, each name/fn pair will be added as methods.

```js
schema.method({
    purr: function () {}
  , scratch: function () {}
});

// later
fizz.purr();
fizz.scratch();

```
<!--sec data-title="源码" data-id="schema_method" data-show=true data-collapse=true ces-->
```js
Schema.prototype.method = function(name, fn) {
  if (typeof name !== 'string') {
    for (var i in name) {
      this.methods[i] = name[i];
    }
  } else {
    this.methods[name] = fn;
  }
  return this;
};
```
<!--endsec-->

## Schema#path(path, constructor)

Gets/sets schema paths.

##### 参数：

  * `path` &lt;[String][]&gt;
  * `constructor` &lt;[Object][]&gt;

Sets a path (if arity 2)
Gets a path (if arity 1)

##### 示例：

```js
schema.path('name') // returns a SchemaType
schema.path('name', Number) // changes the schemaType of `name` to Number
```

<!--sec data-title="源码" data-id="schema_path" data-show=true data-collapse=true ces-->
```js
Schema.prototype.path = function(path, obj) {
  if (obj === undefined) {
    if (this.paths[path]) {
      return this.paths[path];
    }
    if (this.subpaths[path]) {
      return this.subpaths[path];
    }
    if (this.singleNestedPaths[path]) {
      return this.singleNestedPaths[path];
    }

    // subpaths?
    return /\.\d+\.?.*$/.test(path)
        ? getPositionalPath(this, path)
        : undefined;
  }

  // some path names conflict with document methods
  if (reserved[path]) {
    throw new Error('`' + path + '` may not be used as a schema pathname');
  }

  if (warnings[path]) {
    console.log('WARN: ' + warnings[path]);
  }

  // update the tree
  var subpaths = path.split(/\./),
      last = subpaths.pop(),
      branch = this.tree;

  subpaths.forEach(function(sub, i) {
    if (!branch[sub]) {
      branch[sub] = {};
    }
    if (typeof branch[sub] !== 'object') {
      var msg = 'Cannot set nested path `' + path + '`. '
          + 'Parent path `'
          + subpaths.slice(0, i).concat([sub]).join('.')
          + '` already set to type ' + branch[sub].name
          + '.';
      throw new Error(msg);
    }
    branch = branch[sub];
  });

  branch[last] = utils.clone(obj);

  this.paths[path] = Schema.interpretAsType(path, obj, this.options);

  if (this.paths[path].$isSingleNested) {
    for (var key in this.paths[path].schema.paths) {
      this.singleNestedPaths[path + '.' + key] =
          this.paths[path].schema.paths[key];
    }
    for (key in this.paths[path].schema.singleNestedPaths) {
      this.singleNestedPaths[path + '.' + key] =
          this.paths[path].schema.singleNestedPaths[key];
    }

    this.childSchemas.push({
      schema: this.paths[path].schema,
      model: this.paths[path].caster
    });
  } else if (this.paths[path].$isMongooseDocumentArray) {
    this.childSchemas.push({
      schema: this.paths[path].schema,
      model: this.paths[path].casterConstructor
    });
  }
  return this;
};
```
<!--endsec-->

## Schema#pathType(path)

Returns the pathType of path for this schema.

##### 参数：

  * path &lt;[String][]&gt;

##### 返回值：

  * &lt;[String][]&gt;

Given a path, returns whether it is a real, virtual, nested, or ad-hoc/undefined path.

<!--sec data-title="源码" data-id="Schema_pathType" data-show=true data-collapse=true ces-->
```js
Schema.prototype.pathType = function(path) {
  if (path in this.paths) {
    return 'real';
  }
  if (path in this.virtuals) {
    return 'virtual';
  }
  if (path in this.nested) {
    return 'nested';
  }
  if (path in this.subpaths) {
    return 'real';
  }
  if (path in this.singleNestedPaths) {
    return 'real';
  }

  if (/\.\d+\.|\.\d+$/.test(path)) {
    return getPositionalPathType(this, path);
  }
  return 'adhocOrUndefined';
};
```
<!--endsec-->


## Schema#plugin(plugin, [opts])

Registers a plugin for this schema.

##### 参数：

  * `plugin` &lt;[Function][]&gt; callback

  * `[opts]` &lt;[Object][]&gt;

##### 参见：

  * [plugins](/Library/mongoose/docs/plugins.md)


<!--sec data-title="源码" data-id="Schema_plugin" data-show=true data-collapse=true ces-->
```js
Schema.prototype.plugin = function(fn, opts) {
  if (typeof fn !== 'function') {
    throw new Error('First param to `schema.plugin()` must be a function, ' +
      'got "' + (typeof fn) + '"');
  }

  if (opts &&
      opts.deduplicate) {
    for (var i = 0; i < this.plugins.length; ++i) {
      if (this.plugins[i].fn === fn) {
        return this;
      }
    }
  }
  this.plugins.push({ fn: fn, opts: opts });

  fn(this, opts);
  return this;
};
```
<!--endsec-->

## Schema#post(method, fn)

Defines a post hook for the document

##### 参数：

  * `method` &lt;[String][]&gt; name of the method to hook

  * `fn` &lt;[Function][]&gt; callback

##### 参见：

  * [middleware](/Library/mongoose/docs/midlleware.md)

  * [hooks.js](https://www.npmjs.com/package/hooks-fixed)

  * [kareem](http://npmjs.org/package/kareem)

```js
var schema = new Schema(..);
schema.post('save', function (doc) {
  console.log('this fired after a document was saved');
});

schema.post('find', function(docs) {
  console.log('this fired after you run a find query');
});

var Model = mongoose.model('Model', schema);

var m = new Model(..);
m.save(function(err) {
  console.log('this fires after the `post` hook');
});

m.find(function(err, docs) {
  console.log('this fires after the post find hook');
});
```

<!--sec data-title="源码" data-id="Schema_post" data-show=true data-collapse=true ces-->
```js
Schema.prototype.post = function(method, fn) {
  if (IS_KAREEM_HOOK[method]) {
    this.s.hooks.post.apply(this.s.hooks, arguments);
    return this;
  }
  // assuming that all callbacks with arity < 2 are synchronous post hooks
  if (fn.length < 2) {
    return this.queue('on', [arguments[0], function(doc) {
      return fn.call(doc, doc);
    }]);
  }

  if (fn.length === 3) {
    this.s.hooks.post(method + ':error', fn);
    return this;
  }

  return this.queue('post', [arguments[0], function(next) {
    // wrap original function so that the callback goes last,
    // for compatibility with old code that is using synchronous post hooks
    var _this = this;
    var args = Array.prototype.slice.call(arguments, 1);
    fn.call(this, this, function(err) {
      return next.apply(_this, [err].concat(args));
    });
  }]);
};
```
<!--endsec-->

## Schema#pre(method, callback)

Defines a pre hook for the document.

##### 参数：

  * `method` &lt;[String][]&gt;

  * `callback` &lt;[Function][]&gt;

##### 参见：

  * [hooks.js](https://github.com/bnoguchi/hooks-js/tree/31ec571cef0332e21121ee7157e0cf9728572cc3)

##### 示例：

```js
var toySchema = new Schema(..);

toySchema.pre('save', function (next) {
  if (!this.created) this.created = new Date;
  next();
})

toySchema.pre('validate', function (next) {
  if (this.name !== 'Woody') this.name = 'Woody';
  next();
})
```
<!--sec data-title="源码" data-id="Schema_pre" data-show=true data-collapse=true ces-->
```js
Schema.prototype.pre = function() {
  var name = arguments[0];
  if (IS_KAREEM_HOOK[name]) {
    this.s.hooks.pre.apply(this.s.hooks, arguments);
    return this;
  }
  return this.queue('pre', arguments);
};
```
<!--endsec-->

## Schema#queue(name, args)

Adds a method call to the queue.

##### 参数：

  * name &lt;[String][]&gt; name of the document method to call later

  * args &lt;[Array][]&gt; arguments to pass to the method


<!--sec data-title="源码" data-id="Schema_queue" data-show=true data-collapse=true ces-->
```js
Schema.prototype.queue = function(name, args) {
  this.callQueue.push([name, args]);
  return this;
};
```
<!--endsec-->

## Schema#remove(path)

Removes the given path (or [paths]).

##### 参数：

  * path <String, Array>
  *
<!--sec data-title="源码" data-id="Schema_remove" data-show=true data-collapse=true ces-->
```js
Schema.prototype.remove = function(path) {
  if (typeof path === 'string') {
    path = [path];
  }
  if (Array.isArray(path)) {
    path.forEach(function(name) {
      if (this.path(name)) {
        delete this.paths[name];

        var pieces = name.split('.');
        var last = pieces.pop();
        var branch = this.tree;
        for (var i = 0; i < pieces.length; ++i) {
          branch = branch[pieces[i]];
        }
        delete branch[last];
      }
    }, this);
  }
};
```
<!--endsec-->

## Schema#requiredPaths(invalidate)

Returns an Array of path strings that are required by this schema.

##### 参数：

  * invalidate &lt;[Boolean][]&gt; refresh the cache

##### 返回值：

  * &lt;[Array][]&gt;

<!--sec data-title="源码" data-id="Schema_requiredPaths" data-show=true data-collapse=true ces-->
```js
Schema.prototype.requiredPaths = function requiredPaths(invalidate) {
  if (this._requiredpaths && !invalidate) {
    return this._requiredpaths;
  }

  var paths = Object.keys(this.paths),
      i = paths.length,
      ret = [];

  while (i--) {
    var path = paths[i];
    if (this.paths[path].isRequired) {
      ret.push(path);
    }
  }
  this._requiredpaths = ret;
  return this._requiredpaths;
};
```
<!--endsec-->


## Schema(definition, [options])

Schema constructor.

##### 参数：

  * `definition` &lt;[Object][]&gt;

  * `[options]` &lt;[Object][]&gt;

##### 继承：

  * [NodeJS EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)

##### 事件：

  * `init`: Emitted after the schema is compiled into a Model.

##### 示例：

```js
var child = new Schema({ name: String });
var schema = new Schema({ name: String, age: Number, children: [child] });
var Tree = mongoose.model('Tree', schema);

// setting schema options
new Schema({ name: String }, { _id: false, autoIndex: false })
```

##### 选项:

  * [autoIndex][]: bool - defaults to null (which means use the connection's autoIndex option)
  * [bufferCommands][]: bool - defaults to true
  * [capped][]: bool - defaults to false
  * [collection][]: string - no default
  * [emitIndexErrors][]: bool - defaults to false.
  * [id][]: bool - defaults to true
  * [_id][]: bool - defaults to true
  * [minimize][]: bool - controls document#toObject behavior when called manually - defaults to true
  * [read][]: string
  * [safe][]: bool - defaults to true.
  * [shardKey][]: bool - defaults to null
  * [strict][]: bool - defaults to true
  * [toJSON][] - object - no default
  * [toObject][] - object - no default
  * [typeKey][] - string - defaults to 'type'
  * [useNestedStrict][] - boolean - defaults to false
  * [validateBeforeSave][] - bool - defaults to true
  * [versionKey][]: string - defaults to "__v"
  * [collation][]: object - defaults to null (which means use no collation)

  [autoIndex]: /Library/mongoose/docs/guide.md#autoIndex
  [bufferCommands]: /Library/mongoose/docs/guide.md#bufferCommands
  [capped]: /Library/mongoose/docs/guide.md#capped
  [collection]: /Library/mongoose/docs/guide.md#collection
  [emitIndexErrors]: /Library/mongoose/docs/guide.md#emitIndexErrors
  [id]: /Library/mongoose/docs/guide.md#id
  [_id]: /Library/mongoose/docs/guide.md#_id
  [minimize]:
  [read]: /Library/mongoose/docs/guide.md#read
  [safe]: /Library/mongoose/docs/guide.md#safe
  [shardKey]: /Library/mongoose/docs/guide.md#shardKey
  [strict]: /Library/mongoose/docs/guide.md#strict
  [toJSON]: /Library/mongoose/docs/guide.md#toJSON
  [toObject]: /Library/mongoose/docs/guide.md#toObject
  [typeKey]: /Library/mongoose/docs/guide.md#typeKey
  [useNestedStrict]: /Library/mongoose/docs/guide.md#useNestedStrict
  [validateBeforeSave]: /Library/mongoose/docs/guide.md#validateBeforeSave
  [versionKey]: /Library/mongoose/docs/guide.md#versionKey
  [collation]: /Library/mongoose/docs/guide.md#collation

##### 注意：

When nesting schemas, (children in the example above), always declare the child schema first before passing it into its parent.

<!--sec data-title="源码" data-id="Schema" data-show=true data-collapse=true ces-->
```js
function Schema(obj, options) {
  if (!(this instanceof Schema)) {
    return new Schema(obj, options);
  }

  this.obj = obj;
  this.paths = {};
  this.aliases = {};
  this.subpaths = {};
  this.virtuals = {};
  this.singleNestedPaths = {};
  this.nested = {};
  this.inherits = {};
  this.callQueue = [];
  this._indexes = [];
  this.methods = {};
  this.statics = {};
  this.tree = {};
  this.query = {};
  this.childSchemas = [];
  this.plugins = [];

  this.s = {
    hooks: new Kareem(),
    kareemHooks: IS_KAREEM_HOOK
  };

  this.options = this.defaultOptions(options);

  // build paths
  if (obj) {
    this.add(obj);
  }

  // check if _id's value is a subdocument (gh-2276)
  var _idSubDoc = obj && obj._id && utils.isObject(obj._id);

  // ensure the documents get an auto _id unless disabled
  var auto_id = !this.paths['_id'] &&
      (!this.options.noId && this.options._id) && !_idSubDoc;

  if (auto_id) {
    var _obj = {_id: {auto: true}};
    _obj._id[this.options.typeKey] = Schema.ObjectId;
    this.add(_obj);
  }

  for (var i = 0; i < this._defaultMiddleware.length; ++i) {
    var m = this._defaultMiddleware[i];
    this[m.kind](m.hook, !!m.isAsync, m.fn);
  }

  if (this.options.timestamps) {
    this.setupTimestamp(this.options.timestamps);
  }

  // Assign virtual properties based on alias option
  aliasFields(this);
}
```
<!--endsec-->

## Schema#set(key, [value])

Sets/gets a schema option.

##### 参数：

  * key &lt;[String][]&gt; option name

  * [value] &lt;[Object][]&gt; if not passed, the current option value is returned

##### 参见：

* [Schema](/Library/mongoose/docs/guide.md)


##### 示例：

```js
schema.set('strict'); // 'true' by default
schema.set('strict', false); // Sets 'strict' to false
schema.set('strict'); // 'false'
```
<!--sec data-title="源码" data-id="Schema_set" data-show=true data-collapse=true ces-->
```js
Schema.prototype.set = function(key, value, _tags) {
  if (arguments.length === 1) {
    return this.options[key];
  }

  switch (key) {
    case 'read':
      this.options[key] = readPref(value, _tags);
      break;
    case 'safe':
      this.options[key] = value === false
          ? {w: 0}
          : value;
      break;
    case 'timestamps':
      this.setupTimestamp(value);
      this.options[key] = value;
      break;
    default:
      this.options[key] = value;
  }

  return this;
};
```
<!--endsec-->


## Schema#static(name, [fn])

Adds static "class" methods to Models compiled from this schema.

##### 参数：

  * `name` <String, Object>

  * `[fn]` &lt;[Function][]&gt;

##### 示例：

```js
var schema = new Schema(..);
schema.static('findByName', function (name, callback) {
  return this.find({ name: name }, callback);
});

var Drink = mongoose.model('Drink', schema);
Drink.findByName('sanpellegrino', function (err, drinks) {
  //
});
```

If a hash of name/fn pairs is passed as the only argument, each name/fn pair will be added as statics.

<!--sec data-title="源码" data-id="Schema_static" data-show=true data-collapse=true ces-->
```js
Schema.prototype.static = function(name, fn) {
  if (typeof name !== 'string') {
    for (var i in name) {
      this.statics[i] = name[i];
    }
  } else {
    this.statics[name] = fn;
  }
  return this;
};
```
<!--endsec-->


## Schema#virtual(name, [options])

Creates a virtual type with the given name.

##### 参数：

  * name &lt;[String][]&gt;

  * [options] &lt;[Object][]&gt;

##### 返回值：

  * <VirtualType>


<!--sec data-title="源码" data-id="Schema_virtual" data-show=true data-collapse=true ces-->
```js
Schema.prototype.virtual = function(name, options) {
  if (options && options.ref) {
    if (!options.localField) {
      throw new Error('Reference virtuals require `localField` option');
    }

    if (!options.foreignField) {
      throw new Error('Reference virtuals require `foreignField` option');
    }

    this.pre('init', function(next, obj) {
      if (mpath.has(name, obj)) {
        var _v = mpath.get(name, obj);
        if (!this.$$populatedVirtuals) {
          this.$$populatedVirtuals = {};
        }

        if (options.justOne) {
          this.$$populatedVirtuals[name] = Array.isArray(_v) ?
            _v[0] :
            _v;
        } else {
          this.$$populatedVirtuals[name] = Array.isArray(_v) ?
            _v :
            _v == null ? [] : [_v];
        }

        mpath.unset(name, obj);
      }
      if (this.ownerDocument) {
        next();
        return this;
      } else {
        next();
      }
    });

    var virtual = this.virtual(name);
    virtual.options = options;
    return virtual.
      get(function() {
        if (!this.$$populatedVirtuals) {
          this.$$populatedVirtuals = {};
        }
        if (name in this.$$populatedVirtuals) {
          return this.$$populatedVirtuals[name];
        }
        return null;
      }).
      set(function(_v) {
        if (!this.$$populatedVirtuals) {
          this.$$populatedVirtuals = {};
        }

        if (options.justOne) {
          this.$$populatedVirtuals[name] = Array.isArray(_v) ?
            _v[0] :
            _v;

          if (typeof this.$$populatedVirtuals[name] !== 'object') {
            this.$$populatedVirtuals[name] = null;
          }
        } else {
          this.$$populatedVirtuals[name] = Array.isArray(_v) ?
            _v :
            _v == null ? [] : [_v];

          this.$$populatedVirtuals[name] = this.$$populatedVirtuals[name].filter(function(doc) {
            return doc && typeof doc === 'object';
          });
        }
      });
  }

  var virtuals = this.virtuals;
  var parts = name.split('.');

  if (this.pathType(name) === 'real') {
    throw new Error('Virtual path "' + name + '"' +
      ' conflicts with a real path in the schema');
  }

  virtuals[name] = parts.reduce(function(mem, part, i) {
    mem[part] || (mem[part] = (i === parts.length - 1)
        ? new VirtualType(options, name)
        : {});
    return mem[part];
  }, this.tree);

  return virtuals[name];
};

```
<!--endsec-->
## Schema#virtualpath(name)

Returns the virtual type with the given name.

##### 参数：

  * name &lt;[String][]&gt;

##### 返回值：

  * <VirtualType>


<!--sec data-title="源码" data-id="Schema_virtualpath" data-show=true data-collapse=true ces-->
```js
Schema.prototype.virtualpath = function(name) {
  return this.virtuals[name];
};
```
<!--endsec-->

## Schema.indexTypes()

The allowed index types

<!--sec data-title="源码" data-id="createConnection" data-show=true data-collapse=true ces-->
```js
var indexTypes = '2d 2dsphere hashed text'.split(' ');

Object.defineProperty(Schema, 'indexTypes', {
  get: function() {
    return indexTypes;
  },
  set: function() {
    throw new Error('Cannot overwrite Schema.indexTypes');
  }
});
```
<!--endsec-->

## Schema.reserved

Reserved document keys.

<!--sec data-title="源码" data-id="Schema_reserved" data-show=true data-collapse=true ces-->
```js
Schema.reserved = Object.create(null);
var reserved = Schema.reserved;
// Core object
reserved['prototype'] =
// EventEmitter
reserved.emit =
reserved.on =
reserved.once =
reserved.listeners =
reserved.removeListener =
// document properties and functions
reserved.collection =
reserved.db =
reserved.errors =
reserved.init =
reserved.isModified =
reserved.isNew =
reserved.get =
reserved.modelName =
reserved.save =
reserved.schema =
reserved.toObject =
reserved.validate =
reserved.remove =
// hooks.js
reserved._pres = reserved._posts = 1;

```
<!--endsec-->

Keys in this object are names that are rejected in schema declarations b/c they conflict with mongoose functionality. Using these key name will throw an error.

```
on, emit, _events, db, get, set, init, isNew, errors, schema, options, modelName, collection, _pres, _posts, toObject
```

##### 注意：

Use of these terms as method names is permitted, but play at your own risk, as they may be existing mongoose document methods you are stomping on.

```js
var schema = new Schema(..);
 schema.methods.init = function () {} // potentially breaking
```

## Schema.Types

The various built-in Mongoose Schema Types.

<!--sec data-title="源码" data-id="Schema_Types" data-show=true data-collapse=true ces-->
```js
Schema.Types = MongooseTypes = require('./schema/index');
```
<!--endsec-->


##### 示例：

```js
var mongoose = require('mongoose');
var ObjectId = mongoose.Schema.Types.ObjectId;

```

##### 类型：

  * [String]()
  * [Number]()
  * [Boolean]() | Bool
  * [Array]()
  * [Buffer]()
  * [Date]()
  * [ObjectId]() | Oid
  * [Mixed]()

Using this exposed access to the Mixed SchemaType, we can use them in our schema.

```js
var Mixed = mongoose.Schema.Types.Mixed;
new mongoose.Schema({ _user: Mixed })
```

## Schema#childSchemas

Array of child schemas (from document arrays and single nested subdocs)
and their corresponding compiled models. Each element of the array is
an object with 2 properties: schema and model.

This property is typically only useful for plugin authors and advanced users.
You do not need to interact with this property at all to use mongoose.

<!--sec data-title="源码" data-id="Schema_childSchemas" data-show=true data-collapse=true ces-->
```js
Object.defineProperty(Schema.prototype, 'childSchemas', {
  configurable: false,
  enumerable: true,
  writable: true
});
```
<!--endsec-->


## Schema#obj

The original object passed to the schema constructor

##### 示例：

```js
var schema = new Schema({ a: String }).add({ b: String });
schema.obj; // { a: String }
```
<!--sec data-title="源码" data-id="Schema_obj" data-show=true data-collapse=true ces-->
```js
Schema.prototype.obj;
```
<!--endsec-->


# document.js

> 源码：[document.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/document.js)


## MISSING method name

Getter/setter, determines whether the document was removed or not.

##### 参数：

  * [val] &lt;[Boolean][]&gt; optional, overrides whether mongoose thinks the doc is deleted

##### 返回值：

  * &lt;[Boolean][]&gt; whether mongoose thinks this doc is deleted.

##### 示例：

```js
product.remove(function (err, product) {
  product.isDeleted(); // true
  product.remove(); // no-op, doesn't send anything to the db

  product.isDeleted(false);
  product.isDeleted(); // false
  product.remove(); // will execute a remove against the db
})
```
<!--sec data-title="源码" data-id="MISSING_method_name" data-show=true data-collapse=true ces-->
```js
Document.prototype.$isDeleted = function(val) {
  if (arguments.length === 0) {
    return !!this.$__.isDeleted;
  }

  this.$__.isDeleted = !!val;
  return this;
};
```
<!--endsec-->


## MISSING method name

Alias for set(), used internally to avoid conflicts

##### 参数：

  * `path` <String, Object> path or object of key/vals to set

  * `val` &lt;[Any][]&gt; the value to set

  * `[type]` <Schema, String, Number, Buffer, *> optionally specify a type for "on-the-fly" attributes

  * `[options]` &lt;[Object][]&gt; optionally specify options that modify the behavior of the set

<!--sec data-title="源码" data-id="MISSING_method_name2" data-show=true data-collapse=true ces-->
```js
Document.prototype.$set = function(path, val, type, options) {
  if (type && utils.getFunctionName(type.constructor) === 'Object') {
    options = type;
    type = undefined;
  }

  options = options || {};
  var merge = options.merge;
  var adhoc = type && type !== true;
  var constructing = type === true;
  var adhocs;

  var strict = 'strict' in options
      ? options.strict
      : this.$__.strictMode;

  if (adhoc) {
    adhocs = this.$__.adhocPaths || (this.$__.adhocPaths = {});
    adhocs[path] = Schema.interpretAsType(path, type, this.schema.options);
  }

  if (typeof path !== 'string') {
    // new Document({ key: val })

    if (path === null || path === void 0) {
      var _ = path;
      path = val;
      val = _;
    } else {
      var prefix = val
          ? val + '.'
          : '';

      if (path instanceof Document) {
        if (path.$__isNested) {
          path = path.toObject();
        } else {
          path = path._doc;
        }
      }

      var keys = Object.keys(path);
      var len = keys.length;
      var i = 0;
      var pathtype;
      var key;

      if (len === 0 && !this.schema.options.minimize) {
        if (val) {
          this.$set(val, {});
        }
        return this;
      }

      if (this.schema.options.retainKeyOrder) {
        while (i < len) {
          _handleIndex.call(this, i++);
        }
      } else {
        while (len--) {
          _handleIndex.call(this, len);
        }
      }

      return this;
    }
  }

  function _handleIndex(i) {
    key = keys[i];
    var pathName = prefix + key;
    pathtype = this.schema.pathType(pathName);

    if (path[key] !== null
        && path[key] !== void 0
          // need to know if plain object - no Buffer, ObjectId, ref, etc
        && utils.isObject(path[key])
        && (!path[key].constructor || utils.getFunctionName(path[key].constructor) === 'Object')
        && pathtype !== 'virtual'
        && pathtype !== 'real'
        && !(this.$__path(pathName) instanceof MixedSchema)
        && !(this.schema.paths[pathName] &&
        this.schema.paths[pathName].options &&
        this.schema.paths[pathName].options.ref)) {
      this.$set(path[key], prefix + key, constructing);
    } else if (strict) {
      // Don't overwrite defaults with undefined keys (gh-3981)
      if (constructing && path[key] === void 0 &&
          this.get(key) !== void 0) {
        return;
      }

      if (pathtype === 'real' || pathtype === 'virtual') {
        // Check for setting single embedded schema to document (gh-3535)
        var p = path[key];
        if (this.schema.paths[pathName] &&
            this.schema.paths[pathName].$isSingleNested &&
            path[key] instanceof Document) {
          p = p.toObject({ virtuals: false, transform: false });
        }
        this.$set(prefix + key, p, constructing);
      } else if (pathtype === 'nested' && path[key] instanceof Document) {
        this.$set(prefix + key,
            path[key].toObject({transform: false}), constructing);
      } else if (strict === 'throw') {
        if (pathtype === 'nested') {
          throw new ObjectExpectedError(key, path[key]);
        } else {
          throw new StrictModeError(key);
        }
      }
    } else if (path[key] !== void 0) {
      this.$set(prefix + key, path[key], constructing);
    }
  }

  var pathType = this.schema.pathType(path);
  if (pathType === 'nested' && val) {
    if (utils.isObject(val) &&
        (!val.constructor || utils.getFunctionName(val.constructor) === 'Object')) {
      if (!merge) {
        this.setValue(path, null);
        cleanModifiedSubpaths(this, path);
      }

      if (Object.keys(val).length === 0) {
        this.setValue(path, {});
        this.markModified(path);
        cleanModifiedSubpaths(this, path);
      } else {
        this.$set(val, path, constructing);
      }
      return this;
    }
    this.invalidate(path, new MongooseError.CastError('Object', val, path));
    return this;
  }

  var schema;
  var parts = path.split('.');

  if (pathType === 'adhocOrUndefined' && strict) {
    // check for roots that are Mixed types
    var mixed;

    for (i = 0; i < parts.length; ++i) {
      var subpath = parts.slice(0, i + 1).join('.');
      schema = this.schema.path(subpath);
      if (schema instanceof MixedSchema) {
        // allow changes to sub paths of mixed types
        mixed = true;
        break;
      }

      // If path is underneath a virtual, bypass everything and just set it.
      if (i + 1 < parts.length && this.schema.pathType(subpath) === 'virtual') {
        mpath.set(path, val, this);
        return this;
      }
    }

    if (!mixed) {
      if (strict === 'throw') {
        throw new StrictModeError(path);
      }
      return this;
    }
  } else if (pathType === 'virtual') {
    schema = this.schema.virtualpath(path);
    schema.applySetters(val, this);
    return this;
  } else {
    schema = this.$__path(path);
  }

  // gh-4578, if setting a deeply nested path that doesn't exist yet, create it
  var cur = this._doc;
  var curPath = '';
  for (i = 0; i < parts.length - 1; ++i) {
    cur = cur[parts[i]];
    curPath += (curPath.length > 0 ? '.' : '') + parts[i];
    if (!cur) {
      this.$set(curPath, {});
      // Hack re: gh-5800. If nested field is not selected, it probably exists
      // so `MongoError: cannot use the part (nested of nested.num) to
      // traverse the element ({nested: null})` is not likely. If user gets
      // that error, its their fault for now. We should reconsider disallowing
      // modifying not selected paths for v5.
      if (!this.isSelected(curPath)) {
        this.unmarkModified(curPath);
      }
      cur = this.getValue(curPath);
    }
  }

  var pathToMark;

  // When using the $set operator the path to the field must already exist.
  // Else mongodb throws: "LEFT_SUBFIELD only supports Object"

  if (parts.length <= 1) {
    pathToMark = path;
  } else {
    for (i = 0; i < parts.length; ++i) {
      subpath = parts.slice(0, i + 1).join('.');
      if (this.isDirectModified(subpath) // earlier prefixes that are already
            // marked as dirty have precedence
          || this.get(subpath) === null) {
        pathToMark = subpath;
        break;
      }
    }

    if (!pathToMark) {
      pathToMark = path;
    }
  }

  // if this doc is being constructed we should not trigger getters
  var priorVal = constructing ?
    undefined :
    this.getValue(path);

  if (!schema) {
    this.$__set(pathToMark, path, constructing, parts, schema, val, priorVal);
    return this;
  }

  var shouldSet = true;
  try {
    // If the user is trying to set a ref path to a document with
    // the correct model name, treat it as populated
    var didPopulate = false;
    if (schema.options &&
        schema.options.ref &&
        val instanceof Document &&
        (schema.options.ref === val.constructor.modelName || schema.options.ref === val.constructor.baseModelName)) {
      if (this.ownerDocument) {
        this.ownerDocument().populated(this.$__fullPath(path),
          val._id, {model: val.constructor});
      } else {
        this.populated(path, val._id, {model: val.constructor});
      }
      didPopulate = true;
    }

    var popOpts;
    if (schema.options &&
        Array.isArray(schema.options[this.schema.options.typeKey]) &&
        schema.options[this.schema.options.typeKey].length &&
        schema.options[this.schema.options.typeKey][0].ref &&
        Array.isArray(val) &&
        val.length > 0 &&
        val[0] instanceof Document &&
        val[0].constructor.modelName &&
        (schema.options[this.schema.options.typeKey][0].ref === val[0].constructor.baseModelName || schema.options[this.schema.options.typeKey][0].ref === val[0].constructor.modelName)) {
      if (this.ownerDocument) {
        popOpts = { model: val[0].constructor };
        this.ownerDocument().populated(this.$__fullPath(path),
          val.map(function(v) { return v._id; }), popOpts);
      } else {
        popOpts = { model: val[0].constructor };
        this.populated(path, val.map(function(v) { return v._id; }), popOpts);
      }
      didPopulate = true;
    }

    var setterContext = constructing && this.$__.$options.priorDoc ?
      this.$__.$options.priorDoc :
      this;
    val = schema.applySetters(val, setterContext, false, priorVal);

    if (!didPopulate && this.$__.populated) {
      delete this.$__.populated[path];
    }

    this.$markValid(path);
  } catch (e) {
    this.invalidate(path,
      new MongooseError.CastError(schema.instance, val, path, e));
    shouldSet = false;
  }

  if (shouldSet) {
    this.$__set(pathToMark, path, constructing, parts, schema, val, priorVal);
  }

  if (schema.$isSingleNested && (this.isDirectModified(path) || val == null)) {
    cleanModifiedSubpaths(this, path);
  }

  return this;
};

```
<!--endsec-->


## Document#$ignore(path)

Don't run validation on this path or persist changes to this path.

##### 参数：

  * `path` &lt;[String][]&gt; the path to ignore

##### 示例：

```js
doc.foo = null;
doc.$ignore('foo');
doc.save() // changes to foo will not be persisted and validators won't be run
```

## Document#$isDefault([path])

Checks if a path is set to its default.

##### 参数：

  * [path] &lt;[String][]&gt;

##### 返回值：

  * &lt;[Boolean][]&gt;

##### 示例：

```js
MyModel = mongoose.model('test', { name: { type: String, default: 'Val '} });
var m = new MyModel();
m.$isDefault('name'); // true
```

## Document#depopulate(path)

Takes a populated field and returns it to its unpopulated state.

##### 参数：

  * `path` &lt;[String][]&gt;

##### 返回值：

  * <Document> this

##### 参见：

  * [Document.populate]()

##### 示例：

```js
Model.findOne().populate('author').exec(function (err, doc) {
  console.log(doc.author.name); // Dr.Seuss
  console.log(doc.depopulate('author'));
  console.log(doc.author); // '5144cf8050f071d979c118a7'
})
```

If the path was not populated, this is a no-op.

<!--sec data-title="源码" data-id="Document_depopulate" data-show=true data-collapse=true ces-->
```js
Document.prototype.depopulate = function(path) {
  if (typeof path === 'string') {
    path = path.split(' ');
  }
  for (var i = 0; i < path.length; i++) {
    var populatedIds = this.populated(path[i]);
    if (!populatedIds) {
      continue;
    }
    delete this.$__.populated[path[i]];
    this.$set(path[i], populatedIds);
  }
  return this;
};
```
<!--endsec-->

## Document#equals(doc)

Returns true if the Document stores the same data as doc.

##### 参数：

  * `doc` <Document> a document to compare

##### 返回值：

  * &lt;[Boolean][]&gt;

Documents are considered equal when they have matching _ids, unless neither
document has an _id, in which case this function falls back to using
deepEqual().

<!--sec data-title="源码" data-id="Document_equals" data-show=true data-collapse=true ces-->
```js
Document.prototype.equals = function(doc) {
  if (!doc) {
    return false;
  }

  var tid = this.get('_id');
  var docid = doc.get ? doc.get('_id') : doc;
  if (!tid && !docid) {
    return deepEqual(this, doc);
  }
  return tid && tid.equals
      ? tid.equals(docid)
      : tid === docid;
};
```
<!--endsec-->

## Document#execPopulate()

Explicitly executes population and returns a promise. Useful for ES2015
integration.

##### 返回值：

  * <Promise> promise that resolves to the document when population is done

##### 参见：

  * [Document.populate]()

##### 示例：

```js
var promise = doc.
  populate('company').
  populate({
    path: 'notes',
    match: /airline/,
    select: 'text',
    model: 'modelName'
    options: opts
  }).
  execPopulate();

// summary
doc.execPopulate().then(resolve, reject);
```

<!--sec data-title="源码" data-id="Document_execPopulate" data-show=true data-collapse=true ces-->
```js
Document.prototype.execPopulate = function() {
  var Promise = PromiseProvider.get();
  var _this = this;
  return new Promise.ES6(function(resolve, reject) {
    _this.populate(function(error, res) {
      if (error) {
        reject(error);
      } else {
        resolve(res);
      }
    });
  });
};
```
<!--endsec-->


## Document#get(path, [type])

Returns the value of a path.

##### 参数：

  * path &lt;[String][]&gt;

  * [type] <Schema, String, Number, Buffer, *> optionally specify a type for on-the-fly attributes

##### 示例：

```js
// path
doc.get('age') // 47

// dynamic casting to a string
doc.get('age', String) // "47"
```

<!--sec data-title="源码" data-id="Document_get" data-show=true data-collapse=true ces-->
```js
Document.prototype.get = function(path, type) {
  var adhoc;
  if (type) {
    adhoc = Schema.interpretAsType(path, type, this.schema.options);
  }

  var schema = this.$__path(path) || this.schema.virtualpath(path);
  var pieces = path.split('.');
  var obj = this._doc;

  if (schema instanceof VirtualType) {
    return schema.applyGetters(null, this);
  }

  for (var i = 0, l = pieces.length; i < l; i++) {
    obj = obj === null || obj === void 0
        ? undefined
        : obj[pieces[i]];
  }

  if (adhoc) {
    obj = adhoc.cast(obj);
  }

  if (schema) {
    obj = schema.applyGetters(obj, this);
  }

  return obj;
};
```
<!--endsec-->

## Document#init(doc, fn)

Initializes the document without setters or marking anything modified.

##### 参数：

  * `doc` &lt;[Object][]&gt; document returned by mongo

  * `fn` &lt;[Function][]&gt; callback

Called internally after a document is returned from mongodb.

<!--sec data-title="源码" data-id="Document_init" data-show=true data-collapse=true ces-->
```js
Document.prototype.init = function(doc, opts, fn) {
  // do not prefix this method with $__ since its
  // used by public hooks

  if (typeof opts === 'function') {
    fn = opts;
    opts = null;
  }

  this.isNew = false;
  this.$init = true;

  // handle docs with populated paths
  // If doc._id is not null or undefined
  if (doc._id !== null && doc._id !== undefined &&
    opts && opts.populated && opts.populated.length) {
    var id = String(doc._id);
    for (var i = 0; i < opts.populated.length; ++i) {
      var item = opts.populated[i];
      if (item.isVirtual) {
        this.populated(item.path, utils.getValue(item.path, doc), item);
      } else {
        this.populated(item.path, item._docs[id], item);
      }
    }
  }

  init(this, doc, this._doc);

  this.emit('init', this);
  this.constructor.emit('init', this);

  this.$__._id = this._id;

  if (fn) {
    fn(null);
  }
  return this;
};

```
<!--endsec-->

## Document#inspect()

Helper for console.log

<!--sec data-title="源码" data-id="Document_inspect" data-show=true data-collapse=true ces-->
```js
Document.prototype.inspect = function(options) {
  var isPOJO = options &&
    utils.getFunctionName(options.constructor) === 'Object';
  var opts;
  if (isPOJO) {
    opts = options;
    opts.minimize = false;
    opts.retainKeyOrder = true;
  }
  return this.toObject(opts);
};
```
<!--endsec-->

## Document#invalidate(path, errorMsg, value, [kind])

Marks a path as invalid, causing validation to fail.

##### 参数：

  * `path` &lt;[String][]&gt; the field to invalidate

  * `errorMsg` <String, Error> the error which states the reason path was invalid

  * `value` <Object, String, Number, T> optional invalid value

  * `[kind]` &lt;[String][]&gt; optional kind property for the error

##### 返回值：

  * <ValidationError> the current ValidationError, with all currently invalidated paths
The errorMsg argument will become the message of the ValidationError.


The value argument (if passed) will be available through the ValidationError.value property.

```js
doc.invalidate('size', 'must be less than 20', 14);

doc.validate(function (err) {
  console.log(err)
  // prints
  { message: 'Validation failed',
    name: 'ValidationError',
    errors:
     { size:
        { message: 'must be less than 20',
          name: 'ValidatorError',
          path: 'size',
          type: 'user defined',
          value: 14 } } }
})
```

<!--sec data-title="源码" data-id="Document_invalidate" data-show=true data-collapse=true ces-->
```js
Document.prototype.invalidate = function(path, err, val, kind) {
  if (!this.$__.validationError) {
    this.$__.validationError = new ValidationError(this);
  }

  if (this.$__.validationError.errors[path]) {
    return;
  }

  if (!err || typeof err === 'string') {
    err = new ValidatorError({
      path: path,
      message: err,
      type: kind || 'user defined',
      value: val
    });
  }

  if (this.$__.validationError === err) {
    return this.$__.validationError;
  }

  this.$__.validationError.addError(path, err);
  return this.$__.validationError;
};
```
<!--endsec-->

## Document#isDirectModified(path)

Returns true if path was directly set and modified, else false.

##### 参数：

  * path &lt;[String][]&gt;

##### 返回值：

  * &lt;[Boolean][]&gt;

##### 示例：

```js
doc.set('documents.0.title', 'changed');
doc.isDirectModified('documents.0.title') // true
doc.isDirectModified('documents') // false
```

<!--sec data-title="源码" data-id="Document_isDirectModified" data-show=true data-collapse=true ces-->
```js
Document.prototype.isDirectModified = function(path) {
  return (path in this.$__.activePaths.states.modify);
};
```
<!--endsec-->

## Document#isDirectSelected(path)

Checks if path was explicitly selected. If no projection, always returns
true.

##### 参数：

  * `path` &lt;[String][]&gt;

##### 返回值：

  * &lt;[Boolean][]&gt;

##### 示例：

```js
Thing.findOne().select('nested.name').exec(function (err, doc) {
   doc.isDirectSelected('nested.name') // true
   doc.isDirectSelected('nested.otherName') // false
   doc.isDirectSelected('nested')  // false
})
```

<!--sec data-title="源码" data-id="Document_isDirectSelected" data-show=true data-collapse=true ces-->
```js
Document.prototype.isDirectSelected = function isDirectSelected(path) {
  if (this.$__.selected) {
    if (path === '_id') {
      return this.$__.selected._id !== 0;
    }

    var paths = Object.keys(this.$__.selected);
    var i = paths.length;
    var inclusive = null;
    var cur;

    if (i === 1 && paths[0] === '_id') {
      // only _id was selected.
      return this.$__.selected._id === 0;
    }

    while (i--) {
      cur = paths[i];
      if (cur === '_id') {
        continue;
      }
      if (!isDefiningProjection(this.$__.selected[cur])) {
        continue;
      }
      inclusive = !!this.$__.selected[cur];
      break;
    }

    if (inclusive === null) {
      return true;
    }

    if (path in this.$__.selected) {
      return inclusive;
    }

    return !inclusive;
  }

  return true;
};
```
<!--endsec-->

## Document#isInit(path)

Checks if path was initialized.

##### 参数：

  * path &lt;[String][]&gt;

##### 返回值：

  * &lt;[Boolean][]&gt;

<!--sec data-title="源码" data-id="Document_isInit" data-show=true data-collapse=true ces-->
```js
Document.prototype.isInit = function(path) {
  return (path in this.$__.activePaths.states.init);
};
```
<!--endsec-->

## Document#isModified([path])

Returns true if this document was modified, else false.

##### 参数：

  * `[path]` &lt;[String][]&gt; optional

##### 返回值：

  * &lt;[Boolean][]&gt;

If path is given, checks if a path or any full path containing path as part of its path chain has been modified.

##### 示例：

```js
doc.set('documents.0.title', 'changed');
doc.isModified()                      // true
doc.isModified('documents')           // true
doc.isModified('documents.0.title')   // true
doc.isModified('documents otherProp') // true
doc.isDirectModified('documents')     // false
```

<!--sec data-title="源码" data-id="Document_isModified" data-show=true data-collapse=true ces-->
```js
Document.prototype.isModified = function(paths) {
  if (paths) {
    if (!Array.isArray(paths)) {
      paths = paths.split(' ');
    }
    var modified = this.modifiedPaths();
    var directModifiedPaths = Object.keys(this.$__.activePaths.states.modify);
    var isModifiedChild = paths.some(function(path) {
      return !!~modified.indexOf(path);
    });
    return isModifiedChild || paths.some(function(path) {
      return directModifiedPaths.some(function(mod) {
        return mod === path || path.indexOf(mod + '.') === 0;
      });
    });
  }
  return this.$__.activePaths.some('modify');
};
```
<!--endsec-->

## Document#isSelected(path)

Checks if path was selected in the source query which initialized this document.

##### 参数：

  * path &lt;[String][]&gt;

##### 返回值：

  * &lt;[Boolean][]&gt;

##### 示例：

```js
Thing.findOne().select('name').exec(function (err, doc) {
   doc.isSelected('name') // true
   doc.isSelected('age')  // false
})
```
<!--sec data-title="源码" data-id="Document_isSelected" data-show=true data-collapse=true ces-->
```js
Document.prototype.isSelected = function isSelected(path) {
  if (this.$__.selected) {
    if (path === '_id') {
      return this.$__.selected._id !== 0;
    }

    var paths = Object.keys(this.$__.selected);
    var i = paths.length;
    var inclusive = null;
    var cur;

    if (i === 1 && paths[0] === '_id') {
      // only _id was selected.
      return this.$__.selected._id === 0;
    }

    while (i--) {
      cur = paths[i];
      if (cur === '_id') {
        continue;
      }
      if (!isDefiningProjection(this.$__.selected[cur])) {
        continue;
      }
      inclusive = !!this.$__.selected[cur];
      break;
    }

    if (inclusive === null) {
      return true;
    }

    if (path in this.$__.selected) {
      return inclusive;
    }

    i = paths.length;
    var pathDot = path + '.';

    while (i--) {
      cur = paths[i];
      if (cur === '_id') {
        continue;
      }

      if (cur.indexOf(pathDot) === 0) {
        return inclusive || cur !== pathDot;
      }

      if (pathDot.indexOf(cur + '.') === 0) {
        return inclusive;
      }
    }

    return !inclusive;
  }

  return true;
};
```
<!--endsec-->

## Document#markModified(path, [scope])

Marks the path as having pending changes to write to the db.

##### 参数：

  * `path` &lt;[String][]&gt; the path to mark modified

  * `[scope]` <Document> the scope to run validators with

Very helpful when using Mixed types.


##### 示例：

```js
doc.mixed.type = 'changed';
doc.markModified('mixed.type');
doc.save() // changes to mixed.type are now persisted
```

<!--sec data-title="源码" data-id="Document_markModified" data-show=true data-collapse=true ces-->
```js
Document.prototype.markModified = function(path, scope) {
  this.$__.activePaths.modify(path);
  if (scope != null && !this.ownerDocument) {
    this.$__.pathsToScopes[path] = scope;
  }
};
```
<!--endsec-->

## Document#modifiedPaths()

Returns the list of paths that have been modified.

##### 返回值：

  * &lt;[Array][]&gt;
  *
<!--sec data-title="源码" data-id="Document_modifiedPaths" data-show=true data-collapse=true ces-->
```js
Document.prototype.modifiedPaths = function() {
  var directModifiedPaths = Object.keys(this.$__.activePaths.states.modify);
  return directModifiedPaths.reduce(function(list, path) {
    var parts = path.split('.');
    return list.concat(parts.reduce(function(chains, part, i) {
      return chains.concat(parts.slice(0, i).concat(part).join('.'));
    }, []).filter(function(chain) {
      return (list.indexOf(chain) === -1);
    }));
  }, []);
};
```
<!--endsec-->

## Document#populate([path], [callback])

Populates document references, executing the callback when complete.
If you want to use promises instead, use this function with
execPopulate()

##### 参数：

  * `[path]` <String, Object> The path to populate or an options object

  * `[callback]` &lt;[Function][]&gt; When passed, population is invoked

##### 返回值：

  * <Document> this

##### 参见：

  * [Model.populate]()

  * [Document.execPopulate]()

##### 示例：

```js
doc
.populate('company')
.populate({
  path: 'notes',
  match: /airline/,
  select: 'text',
  model: 'modelName'
  options: opts
}, function (err, user) {
  assert(doc._id === user._id) // the document itself is passed
})

// summary
doc.populate(path)                   // not executed
doc.populate(options);               // not executed
doc.populate(path, callback)         // executed
doc.populate(options, callback);     // executed
doc.populate(callback);              // executed
doc.populate(options).execPopulate() // executed, returns promise
```

##### 注意：

Population does not occur unless a callback is passed or you explicitly
call execPopulate().
Passing the same path a second time will overwrite the previous path options.
See [Model.populate()]() for explaination of options.

<!--sec data-title="源码" data-id="Document_populate_" data-show=true data-collapse=true ces-->
```js
Document.prototype.depopulate = function(path) {
  if (typeof path === 'string') {
    path = path.split(' ');
  }
  for (var i = 0; i < path.length; i++) {
    var populatedIds = this.populated(path[i]);
    if (!populatedIds) {
      continue;
    }
    delete this.$__.populated[path[i]];
    this.$set(path[i], populatedIds);
  }
  return this;
};
```
<!--endsec-->


## Document#populated(path)

Gets _id(s) used during population of the given path.

##### 参数：

  * path &lt;[String][]&gt;

##### 返回值：

  * <Array, ObjectId, Number, Buffer, String, undefined>

##### 示例：

```js
Model.findOne().populate('author').exec(function (err, doc) {
  console.log(doc.author.name)         // Dr.Seuss
  console.log(doc.populated('author')) // '5144cf8050f071d979c118a7'
})
```

If the path was not populated, undefined is returned.

<!--sec data-title="源码" data-id="Document_populated" data-show=true data-collapse=true ces-->
```js
Document.prototype.populated = function(path, val, options) {
  // val and options are internal

  if (val === null || val === void 0) {
    if (!this.$__.populated) {
      return undefined;
    }
    var v = this.$__.populated[path];
    if (v) {
      return v.value;
    }
    return undefined;
  }

  // internal

  if (val === true) {
    if (!this.$__.populated) {
      return undefined;
    }
    return this.$__.populated[path];
  }

  this.$__.populated || (this.$__.populated = {});
  this.$__.populated[path] = {value: val, options: options};
  return val;
};

```
<!--endsec-->


## function Object() { [native code] }#save([options], [options.safe], [options.validateBeforeSave], [fn])

Saves this document.

##### 参数：

  * `[options]` &lt;[Object][]&gt; options optional options

  * `[options.safe]` &lt;[Object][]&gt; overrides schema's safe option

  * `[options.validateBeforeSave]` &lt;[Boolean][]&gt; set to false to save without validating.

  * `[fn]` &lt;[Function][]&gt; optional callback

##### 返回值：

  * <Promise> Promise

##### 参见：

  * [middleware](/Library/mongoose/docs/middleware.md)

##### 示例：

```js
product.sold = Date.now();
product.save(function (err, product, numAffected) {
  if (err) ..
})
```
  *
The callback will receive three parameters

  * err if an error occurred
  * product which is the saved product
  * numAffected will be 1 when the document was successfully persisted to MongoDB, otherwise 0. Unless you tweak mongoose's internals, you don't need to worry about checking this parameter for errors - checking err is sufficient to make sure your document was properly saved.


As an extra measure of flow control, save will return a Promise.

##### 示例：

```js
product.save().then(function(product) {
   ...
});
```

For legacy reasons, mongoose stores object keys in reverse order on initial
save. That is, { a: 1, b: 2 } will be saved as { b: 2, a: 1 } in
MongoDB. To override this behavior, set
[the toObject.retainKeyOrder option](http://mongoosejs.com/docs/api.html#document_Document-toObject)
to true on your schema.

## (path, val, [type], [options])

Sets the value of a path, or many paths.

##### 参数：

  * `path` <String, Object> path or object of key/vals to set

  * `val` &lt;[Any][]&gt; the value to set

  * `[type]` <Schema, String, Number, Buffer, *> optionally specify a type for "on-the-fly" attributes

  * `[options]` &lt;[Object][]&gt; optionally specify options that modify the behavior of the set

##### 示例：

```js
// path, value
doc.set(path, value)

// object
doc.set({
    path  : value
  , path2 : {
       path  : value
    }
})

// on-the-fly cast to number
doc.set(path, value, Number)

// on-the-fly cast to string
doc.set(path, value, String)

// changing strict mode behavior
doc.set(path, value, { strict: false });
```

<!--sec data-title="源码" data-id="8" data-show=true data-collapse=true ces-->
```js
Document.prototype.set = Document.prototype.$set;
```
<!--endsec-->


##  Document#toJSON(options)

The return value of this method is used in calls to JSON.stringify(doc).

##### 参数：

  * `options` &lt;[Object][]&gt;

##### 返回值：

  * &lt;[Object][]&gt;

##### 参见：

  * [Document#toObject]()

This method accepts the same options as [Document#toObject](). To apply the options to every document of your schema by default, set your [schemas]() toJSON option to the same argument.

```js
schema.set('toJSON', { virtuals: true })
```

See [schema options](/Library/mongoose/docs/guide.md#toJSON) for details.

<!--sec data-title="源码" data-id="Document_toJSON" data-show=true data-collapse=true ces-->
```js
Document.prototype.toJSON = function(options) {
  return this.$toObject(options, true);
};
```
<!--endsec-->

## Document#toObject([options])


Converts this document into a plain javascript object, ready for storage in MongoDB.

##### 参数：

  * `[options]` &lt;[Object][]&gt;

##### 返回值：

  * &lt;[Object][]&gt; js object

##### 参见：

  * [mongodb.Binary](http://mongodb.github.com/node-mongodb-native/api-bson-generated/binary.html)

Buffers are converted to instances of [mongodb.Binary](http://mongodb.github.com/node-mongodb-native/api-bson-generated/binary.html) for proper storage.

##### 选项：

  * `getters` apply all getters (path and virtual getters)
  * `virtuals` apply virtual getters (can override getters option)
  * `minimize` remove empty objects (defaults to true)
  * `transform` a transform function to apply to the resulting document before returning
  * `depopulate` depopulate any populated paths, replacing them with their original refs (defaults to false)
  * `versionKey` whether to include the version key (defaults to true)
  * `retainKeyOrder` keep the order of object keys. If this is set to true, Object.keys(new Doc({ a: 1, b: 2}).toObject()) will always produce ['a', 'b'] (defaults to false)

##### Getters/Virtuals

Example of only applying path getters

```js
doc.toObject({ getters: true, virtuals: false })
```

Example of only applying virtual getters

```js
doc.toObject({ virtuals: true })
```

Example of applying both path and virtual getters

```js
doc.toObject({ getters: true })
```

To apply these options to every document of your schema by default, set your schemas toObject option to the same argument.

```js
schema.set('toObject', { virtuals: true })
```

##### Transform

We may need to perform a transformation of the resulting object based on some criteria, say to remove some sensitive information or return a custom object. In this case we set the optional transform function.

Transform functions receive three arguments

```js
function (doc, ret, options) {}
```
  * doc The mongoose document which is being converted
  * ret The plain object representation which has been converted
  * options The options in use (either schema options or the options passed inline)

##### 示例：

```js
// specify the transform schema option
if (!schema.options.toObject) schema.options.toObject = {};
schema.options.toObject.transform = function (doc, ret, options) {
  // remove the _id of every document before returning the result
  delete ret._id;
  return ret;
}

// without the transformation in the schema
doc.toObject(); // { _id: 'anId', name: 'Wreck-it Ralph' }

// with the transformation
doc.toObject(); // { name: 'Wreck-it Ralph' }
```

With transformations we can do a lot more than remove properties. We can even return completely new customized objects:

```js
if (!schema.options.toObject) schema.options.toObject = {};
schema.options.toObject.transform = function (doc, ret, options) {
  return { movie: ret.name }
}

// without the transformation in the schema
doc.toObject(); // { _id: 'anId', name: 'Wreck-it Ralph' }

// with the transformation
doc.toObject(); // { movie: 'Wreck-it Ralph' }
```

##### 注意：

*if a transform function returns undefined, the return value will be ignored.*

Transformations may also be applied inline, overridding any transform set in the options:

```js
function xform (doc, ret, options) {
  return { inline: ret.name, custom: true }
}

// pass the transform as an inline option
doc.toObject({ transform: xform }); // { inline: 'Wreck-it Ralph', custom: true }
```

If you want to skip transformations, use transform: false:

```js
if (!schema.options.toObject) schema.options.toObject = {};
schema.options.toObject.hide = '_id';
schema.options.toObject.transform = function (doc, ret, options) {
  if (options.hide) {
    options.hide.split(' ').forEach(function (prop) {
      delete ret[prop];
    });
  }
  return ret;
}

var doc = new Doc({ _id: 'anId', secret: 47, name: 'Wreck-it Ralph' });
doc.toObject();                                        // { secret: 47, name: 'Wreck-it Ralph' }
doc.toObject({ hide: 'secret _id', transform: false });// { _id: 'anId', secret: 47, name: 'Wreck-it Ralph' }
doc.toObject({ hide: 'secret _id', transform: true }); // { name: 'Wreck-it Ralph' }
```

Transforms are applied only to the document and are not applied to sub-documents.

Transforms, like all of these options, are also available for toJSON.

See [schema options](/Library/mongoose/docs/guide.html#toObject) for some more details.

During save, no custom options are applied to the document before being sent to the database.

<!--sec data-title="源码" data-id="Document_toObject" data-show=true data-collapse=true ces-->
```js
Document.prototype.toObject = function(options) {
  return this.$toObject(options);
};
```
<!--endsec-->


## Document#toString()

Helper for console.log

## Document#unmarkModified(path)

Clears the modified state on the specified path.

##### 参数：

  * `path` &lt;[String][]&gt; the path to unmark modified

##### 示例：

```js
doc.foo = 'bar';
doc.unmarkModified('foo');
doc.save() // changes to foo will not be persisted
```

<!--sec data-title="源码" data-id="Document_unmarkModified" data-show=true data-collapse=true ces-->
```js
Document.prototype.unmarkModified = function(path) {
  this.$__.activePaths.init(path);
  delete this.$__.pathsToScopes[path];
};
```
<!--endsec-->


## Document#update(doc, options, callback)

Sends an update command with this document _id as the query selector.

##### 参数：

  * `doc` &lt;[Object][]&gt;

  * `options` &lt;[Object][]&gt;

  * `callback` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 参见：

  * [Model.update]()

##### 示例：

```js
weirdCar.update({$inc: {wheels:1}}, { w: 1 }, callback);
Valid options:
same as in Model.update
```
<!--sec data-title="源码" data-id="Document_update" data-show=true data-collapse=true ces-->
```js
Document.prototype.update = function update() {
  var args = utils.args(arguments);
  args.unshift({_id: this._id});
  return this.constructor.update.apply(this.constructor, args);
};
```
<!--endsec-->


## Document#validate(optional, callback)

Executes registered validation rules for this document.

##### 参数：

  * `optional` &lt;[Object][]&gt; options internal options

  * `callback` &lt;[Function][]&gt; optional callback called after validation completes, passing an error if one occurred

##### 返回值：

  * <Promise> Promise

##### 注意：

This method is called pre save and if a validation rule is violated, save is aborted and the error is returned to your callback.

##### 示例：

```js
doc.validate(function (err) {
  if (err) handleError(err);
  else // validation passed
});
```

<!--sec data-title="源码" data-id="Document_validate" data-show=true data-collapse=true ces-->
```js
Document.prototype.validate = function(options, callback) {
  if (typeof options === 'function') {
    callback = options;
    options = null;
  }

  this.$__validate(callback || function() {});
};
```
<!--endsec-->


## Document#validateSync(pathsToValidate)

Executes registered validation rules (skipping asynchronous validators) for this document.

##### 参数：

  * `pathsToValidate` <Array, string> only validate the given paths

##### 返回值：

  * <MongooseError, undefined> MongooseError if there are errors during validation, or undefined if there is no error.

##### 注意：

This method is useful if you need synchronous validation.

##### 示例：

```js
var err = doc.validateSync();
if ( err ){
  handleError( err );
} else {
  // validation passed
}
```

<!--sec data-title="源码" data-id="Document_validateSync" data-show=true data-collapse=true ces-->
```js
Document.prototype.validateSync = function(pathsToValidate) {
  var _this = this;

  if (typeof pathsToValidate === 'string') {
    pathsToValidate = pathsToValidate.split(' ');
  }

  // only validate required fields when necessary
  var paths = _getPathsToValidate(this);

  if (pathsToValidate && pathsToValidate.length) {
    var tmp = [];
    for (var i = 0; i < paths.length; ++i) {
      if (pathsToValidate.indexOf(paths[i]) !== -1) {
        tmp.push(paths[i]);
      }
    }
    paths = tmp;
  }

  var validating = {};

  paths.forEach(function(path) {
    if (validating[path]) {
      return;
    }

    validating[path] = true;

    var p = _this.schema.path(path);
    if (!p) {
      return;
    }
    if (!_this.$isValid(path)) {
      return;
    }

    var val = _this.getValue(path);
    var err = p.doValidateSync(val, _this);
    if (err) {
      _this.invalidate(path, err, undefined, true);
    }
  });

  var err = _this.$__.validationError;
  _this.$__.validationError = undefined;
  _this.emit('validate', _this);
  _this.constructor.emit('validate', _this);

  if (err) {
    for (var key in err.errors) {
      // Make sure cast errors persist
      if (err.errors[key] instanceof MongooseError.CastError) {
        _this.invalidate(key, err.errors[key]);
      }
    }
  }

  return err;
};
```
<!--endsec-->

## Document.$markValid(path)

Marks a path as valid, removing existing validation errors.

##### 参数：

  * path &lt;[String][]&gt; the field to mark as valid


## Document#errors

Hash containing current validation errors.

<!--sec data-title="源码" data-id="Document_errors" data-show=true data-collapse=true ces-->
```js
Document.prototype.errors;
```
<!--endsec-->


## Document#id

The string version of this documents _id.

##### 注意：
This getter exists on all documents by default. The getter can be disabled by setting the id [option](http://mongoosejs.com/docs/guide.html#id) of its Schema to false at construction time.

new Schema({ name: String }, { id: false });
<!--sec data-title="源码" data-id="Document_id" data-show=true data-collapse=true ces-->
```js
Document.prototype.id;
```
<!--endsec-->

##### 参见：

  * [Schema options](/Library/mongoose/docs/guide.html#options)

## Document#isNew

Boolean flag specifying if the document is new.

<!--sec data-title="源码" data-id="Document_isNew" data-show=true data-collapse=true ces-->
```js
Document.prototype.isNew;
```
<!--endsec-->


## Document#schema

The documents schema.

<!--sec data-title="源码" data-id="Document_schema" data-show=true data-collapse=true ces-->
```js
Document.prototype.schema;
```
<!--endsec-->

----

# query.js

> 源码：[query.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/query.js)


## Query#$where(js)

Specifies a javascript function or expression to pass to MongoDBs query system.

##### 参数：

  * `js` &lt;[String][], [Function][]&gt;javascript string or function

##### 返回值：

  * <Query> this

##### 参见：

  * [$where](http://docs.mongodb.org/manual/reference/operator/where/)

##### 示例：

```js
query.$where('this.comments.length === 10 || this.name.length === 5')

// or

query.$where(function () {
  return this.comments.length === 10 || this.name.length === 5;
})
```

##### 注意：

Only use $where when you have a condition that cannot be met using other MongoDB operators like $lt.
**Be sure to read about all of [its caveats](http://docs.mongodb.org/manual/reference/operator/where/) before using.**

## Query#all([path], val)

Specifies an $all query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 参见：

  * [$all](http://docs.mongodb.org/manual/reference/operator/all/)

When called with one argument, the most recent path passed to where() is used.

## Query#and(array)

Specifies arguments for a $and condition.

##### 参数：

  * `array` &lt;[Array][]&gt; array of conditions

##### 返回值：

  * <Query> this

##### 参见：

  * [$and](http://docs.mongodb.org/manual/reference/operator/and/)

##### 示例：

```js
query.and([{ color: 'green' }, { status: 'ok' }])
```

## Query#batchSize(val)

Specifies the batchSize option.

##### 参数：

  * `val` <Number>

##### 参见：

  * [batchSize](http://docs.mongodb.org/manual/reference/method/cursor.batchSize/)

##### 示例：

```js
query.batchSize(100)
```

##### 注意：

Cannot be used with distinct()


## Query#box(val, Upper)

Specifies a $box condition

##### 参数：

  * `val` &lt;[Object][]&gt;

  * `Upper` <[Array]> Right Coords

##### 返回值：

  * <Query> this

##### 参见：

  * [$box](http://docs.mongodb.org/manual/reference/operator/box/)

  * [within() Query#within](http://mongoosejs.com/docs/api.html#query_Query-within)

  * http://www.mongodb.org/display/DOCS/Geospatial+Indexing

##### 示例：

```js
var lowerLeft = [40.73083, -73.99756]
var upperRight= [40.741404,  -73.988135]

query.where('loc').within().box(lowerLeft, upperRight)
query.box({ ll : lowerLeft, ur : upperRight })
```


## Query#cast(model, [obj])

Casts this query to the schema of model

##### 参数：

  * `model` <Model>

  * `[obj]` &lt;[Object][]&gt;

##### 返回值：

  * &lt;[Object][]&gt;

##### 注意：

If obj is present, it is cast instead of this query.

<!--sec data-title="源码" data-id="Query_cast" data-show=true data-collapse=true ces-->
```js
Query.prototype.cast = function(model, obj) {
  obj || (obj = this._conditions);

  try {
    return cast(model.schema, obj, {
      upsert: this.options && this.options.upsert,
      strict: (this.options && 'strict' in this.options) ?
        this.options.strict :
        (model.schema.options && model.schema.options.strict),
      strictQuery: (this.options && this.options.strictQuery) ||
        (model.schema.options && model.schema.options.strictQuery)
    }, this);
  } catch (err) {
    // CastError, assign model
    if (typeof err.setModel === 'function') {
      err.setModel(model);
    }
    throw err;
  }
};
```
<!--endsec-->


## Query#catch([reject])

Executes the query returning a Promise which will be
resolved with either the doc(s) or rejected with the error.
Like .then(), but only takes a rejection handler.

##### 参数：

  * [reject] &lt;[Function][]&gt;

##### 返回值：

  * <Promise>

<!--sec data-title="源码" data-id="Query_catch" data-show=true data-collapse=true ces-->
```js
Query.prototype.catch = function(reject) {
  return this.exec().then(null, reject);
};
```
<!--endsec-->


## Query#center()

DEPRECATED Alias for [circle]()

**Deprecated.** Use [circle]() instead.


## Query#centerSphere([path], val)

DEPRECATED Specifies a $centerSphere condition

##### 参数：

    * `[path]` &lt;[String][]&gt;

    * `val` &lt;[Object][]&gt;

##### 返回值：

    * <Query> this

##### 参见：

    * http://www.mongodb.org/display/DOCS/Geospatial+Indexing

    * [$centerSphere](http://docs.mongodb.org/manual/reference/operator/centerSphere/)

**Deprecated.** Use [circle]() instead.

##### 示例：

```
var area = { center: [50, 50], radius: 10 };
query.where('loc').within().centerSphere(area);
```
<!--sec data-title="源码" data-id="Query_centerSphere" data-show=true data-collapse=true ces-->
```js
var area = { center: [50, 50], radius: 10 };
query.where('loc').within().centerSphere(area);
```
<!--endsec-->


## Query#circle([path], area)

Specifies a $center or $centerSphere condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `area` &lt;[Object][]&gt;

##### 返回值：

  * <Query> this

##### 参见：

  * [$center](http://docs.mongodb.org/manual/reference/operator/center/)

  * [$centerSphere](http://docs.mongodb.org/manual/reference/operator/centerSphere/)

  * [$geoWithin](http://docs.mongodb.org/manual/reference/operator/geoWithin/)

  * http://www.mongodb.org/display/DOCS/Geospatial+Indexing

##### 示例：

```js
var area = { center: [50, 50], radius: 10, unique: true }
query.where('loc').within().circle(area)
// alternatively
query.circle('loc', area);

// spherical calculations
var area = { center: [50, 50], radius: 10, unique: true, spherical: true }
query.where('loc').within().circle(area)
// alternatively
query.circle('loc', area);
```

New in 3.7.0

## Query#collation(value)

Adds a collation to this op (MongoDB 3.4 and up)

##### 参数：

  * `value` &lt;[Object][]&gt;

##### 返回值：

  * <Query> this

##### 参见：

  * [MongoDB](https://docs.mongodb.com/manual/reference/method/cursor.collation/#cursor.collation)

<!--sec data-title="源码" data-id="Query_collation" data-show=true data-collapse=true ces-->
```js
Query.prototype.collation = function(value) {
  if (this.options == null) {
    this.options = {};
  }
  this.options.collation = value;
  return this;
};
```
<!--endsec-->


## Query#comment(val)

Specifies the comment option.

##### 参数：

  * `val` <Number>

##### 参见：

  * [comment](http://docs.mongodb.org/manual/reference/operator/comment/)

##### 示例：

```js
query.comment('login query')
```

##### 注意：

Cannot be used with distinct()


## Query#count([criteria], [callback])

Specifying this query as a count query.

##### 参数：

  * `[criteria]` &lt;[Object][]&gt; mongodb selector

  * `[callback]` &lt;[Function][]&gt; optional params are (error, count)

##### 返回值：

  * <Query> this

##### 参见：

  * [count](http://docs.mongodb.org/manual/reference/method/db.collection.count/)

Passing a callback executes the query.

**This function triggers the following middleware**

  * count()


##### 示例：

```js
var countQuery = model.where({ 'color': 'black' }).count();

query.count({ color: 'black' }).count(callback)

query.count({ color: 'black' }, callback)

query.where('color', 'black').count(function (err, count) {
  if (err) return handleError(err);
  console.log('there are %d kittens', count);
})
```
<!--sec data-title="源码" data-id="Query_count" data-show=true data-collapse=true ces-->
```js
Query.prototype.count = function(conditions, callback) {
  if (typeof conditions === 'function') {
    callback = conditions;
    conditions = undefined;
  }

  if (mquery.canMerge(conditions)) {
    this.merge(conditions);
  }

  this.op = 'count';
  if (!callback) {
    return this;
  }

  this._count(callback);

  return this;
};
```
<!--endsec-->


## Query#cursor([options])


Returns a wrapper around a [mongodb driver cursor](http://mongodb.github.io/node-mongodb-native/2.1/api/Cursor.html).
A QueryCursor exposes a [Streams3][]-compatible
interface, as well as a .next() function.

[Streams3]: https://strongloop.com/strongblog/whats-new-io-js-beta-streams3/

##### 参数：

  * `[options]` &lt;[Object][]&gt;

##### 返回值：

  * <QueryCursor>

##### 参见：

  * [QueryCursor]()

The `.cursor()` function triggers pre find hooks, but not post find hooks.

##### 示例：

```js
// There are 2 ways to use a cursor. First, as a stream:
Thing.
  find({ name: /^hello/ }).
  cursor().
  on('data', function(doc) { console.log(doc); }).
  on('end', function() { console.log('Done!'); });

// Or you can use `.next()` to manually get the next doc in the stream.
// `.next()` returns a promise, so you can use promises or callbacks.
var cursor = Thing.find({ name: /^hello/ }).cursor();
cursor.next(function(error, doc) {
  console.log(doc);
});

// Because `.next()` returns a promise, you can use co
// to easily iterate through all documents without loading them
// all into memory.
co(function*() {
  const cursor = Thing.find({ name: /^hello/ }).cursor();
  for (let doc = yield cursor.next(); doc != null; doc = yield cursor.next()) {
    console.log(doc);
  }
});
```

##### 可用的选项：

  * `transform`: optional function which accepts a mongoose document. The return value of the function will be emitted on data and returned by .next().


<!--sec data-title="源码" data-id="Query_cursor" data-show=true data-collapse=true ces-->

```js
Query.prototype.cursor = function cursor(opts) {
  this._applyPaths();
  this._fields = this._castFields(this._fields);
  this.setOptions({ fields: this._fieldsForExec() });
  if (opts) {
    this.setOptions(opts);
  }

  try {
    this.cast(this.model);
  } catch (err) {
    return (new QueryCursor(this, this.options))._markError(err);
  }

  return new QueryCursor(this, this.options);
};

// the rest of these are basically to support older Mongoose syntax with mquery
```
<!--endsec-->


## Query#deleteMany([filter], [callback])

Declare and/or execute this query as a deleteMany() operation. Works like
remove, except it deletes every document that matches criteria in the
collection, regardless of the value of single.

##### 参数：

  * `[filter]` <Object, Query> mongodb selector

  * `[callback]` &lt;[Function][]&gt; optional params are (error, writeOpResult)

##### 返回值：

  * <Query> this

##### 参见：

  * [writeOpResult](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#~WriteOpResult)

  * [remove](http://docs.mongodb.org/manual/reference/method/db.collection.remove/)

This function does not trigger any middleware

##### 示例：

```js
Character.deleteMany({ name: /Stark/, age: { $gte: 18 } }, callback)
Character.deleteMany({ name: /Stark/, age: { $gte: 18 } }).then(next)
```

<!--sec data-title="源码" data-id="Query_deleteMany" data-show=true data-collapse=true ces-->
```js
Query.prototype.deleteMany = function(filter, callback) {
  if (typeof filter === 'function') {
    callback = filter;
    filter = null;
  }

  filter = utils.toObject(filter, { retainKeyOrder: true });

  try {
    this.cast(this.model, filter);
    this.merge(filter);
  } catch (err) {
    this.error(err);
  }

  prepareDiscriminatorCriteria(this);

  if (!callback) {
    return Query.base.deleteMany.call(this);
  }

  return this._deleteMany.call(this, callback);
};
```
<!--endsec-->

## Query#deleteOne([filter], [callback])

Declare and/or execute this query as a deleteOne() operation. Works like
remove, except it deletes at most one document regardless of the single
option.

##### 参数：

  * `[filter]` <Object, Query> mongodb selector

  * `[callback]` &lt;[Function][]&gt; optional params are (error, writeOpResult)

##### 返回值：

  * <Query> this

##### 参见：

  * [writeOpResult](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#~WriteOpResult)

  * [remove](http://docs.mongodb.org/manual/reference/method/db.collection.remove/)

This function does not trigger any middleware.

##### 示例：

```js
Character.deleteOne({ name: 'Eddard Stark' }, callback)
Character.deleteOne({ name: 'Eddard Stark' }).then(next)
```

<!--sec data-title="源码" data-id="Query_deleteOne" data-show=true data-collapse=true ces-->
```js
Query.prototype.deleteOne = function(filter, callback) {
  if (typeof filter === 'function') {
    callback = filter;
    filter = null;
  }

  filter = utils.toObject(filter, { retainKeyOrder: true });

  try {
    this.cast(this.model, filter);
    this.merge(filter);
  } catch (err) {
    this.error(err);
  }

  prepareDiscriminatorCriteria(this);

  if (!callback) {
    return Query.base.deleteOne.call(this);
  }

  return this._deleteOne.call(this, callback);
};
```
<!--endsec-->


## Query#distinct([field], [criteria], [callback])

Declares or executes a distict() operation.

##### 参数：

  * `[field]` &lt;[String][]&gt;

  * `[criteria]` <Object, Query>

  * `[callback]` &lt;[Function][]&gt; optional params are (error, arr)

##### 返回值：

  * <Query> this

##### 参见：

  * [distinct](http://docs.mongodb.org/manual/reference/method/db.collection.distinct/)

Passing a `callback` executes the query.

This function does not trigger any middleware.

##### 示例：

```js
distinct(field, conditions, callback)
distinct(field, conditions)
distinct(field, callback)
distinct(field)
distinct(callback)
distinct()
```

<!--sec data-title="源码" data-id="Query_distinct" data-show=true data-collapse=true ces-->
```js
Query.prototype.distinct = function(field, conditions, callback) {
  if (!callback) {
    if (typeof conditions === 'function') {
      callback = conditions;
      conditions = undefined;
    } else if (typeof field === 'function') {
      callback = field;
      field = undefined;
      conditions = undefined;
    }
  }

  conditions = utils.toObject(conditions);

  if (mquery.canMerge(conditions)) {
    this.merge(conditions);
  }

  try {
    this.cast(this.model);
  } catch (err) {
    if (!callback) {
      throw err;
    }
    callback(err);
    return this;
  }

  return Query.base.distinct.call(this, {}, field, callback);
};
```
<!--endsec-->


## Query#elemMatch(path, criteria)

Specifies an $elemMatch condition

##### 参数：

  * `path` <String, Object, Function>

  * `criteria` <Object, Function>

##### 返回值：

  * <Query> this

##### 参见：

  * [$elemMatch](http://docs.mongodb.org/manual/reference/operator/elemMatch/)

##### 示例：

```js
query.elemMatch('comment', { author: 'autobot', votes: {$gte: 5}})

query.where('comment').elemMatch({ author: 'autobot', votes: {$gte: 5}})

query.elemMatch('comment', function (elem) {
  elem.where('author').equals('autobot');
  elem.where('votes').gte(5);
})

query.where('comment').elemMatch(function (elem) {
  elem.where({ author: 'autobot' });
  elem.where('votes').gte(5);
})
```


## Query#equals(val)

Specifies the complementary comparison value for paths specified with where()

##### 参数：

  * `val` &lt;[Object][]&gt;

##### 返回值：

  * <Query> this

##### 示例：

```js
User.where('age').equals(49);


// is the same as

User.where('age', 49);
```

## Query#error(err)

Gets/sets the error flag on this query. If this flag is not null or
undefined, the `exec()` promise will reject without executing.

##### 参数：

  * `err` <Error, null> if set, exec() will fail fast before sending the query to MongoDB

##### 示例：

```js
Query().error(); // Get current error value
Query().error(null); // Unset the current error
Query().error(new Error('test')); // `exec()` will resolve with test
Schema.pre('find', function() {
  if (!this.getQuery().userId) {
    this.error(new Error('Not allowed to query without setting userId'));
  }
});
```

Note that query casting runs **after** hooks, so cast errors will override
custom errors.

##### 示例：

```js
var TestSchema = new Schema({ num: Number });
var TestModel = db.model('Test', TestSchema);
TestModel.find({ num: 'not a number' }).error(new Error('woops')).exec(function(error) {
  // `error` will be a cast error because `num` failed to cast
});
```

<!--sec data-title="源码" data-id="Query_error" data-show=true data-collapse=true ces-->
```js
Query.prototype.error = function error(err) {
  if (arguments.length === 0) {
    return this._error;
  }

  this._error = err;
  return this;
};
```
<!--endsec-->


## Query#exec([operation], [callback])

执行查询

##### 参数：

  * `[operation]` <String, Function>

  * `[callback]` &lt;[Function][]&gt; optional params depend on the function being called

##### 返回值：

  <Promise>

##### 示例：

```js
var promise = query.exec();
var promise = query.exec('update');

query.exec(callback);
query.exec('find', callback);
```

<!--sec data-title="源码" data-id="Query_exec" data-show=true data-collapse=true ces-->
```js
Query.prototype.exec = function exec(op, callback) {
  var Promise = PromiseProvider.get();
  var _this = this;

  if (typeof op === 'function') {
    callback = op;
    op = null;
  } else if (typeof op === 'string') {
    this.op = op;
  }

  var _results;
  var promise = new Promise.ES6(function(resolve, reject) {
    if (!_this.op) {
      resolve();
      return;
    }

    _this[_this.op].call(_this, function(error, res) {
      if (error) {
        reject(error);
        return;
      }
      _results = arguments;
      resolve(res);
    });
  });

  if (callback) {
    promise.then(
      function() {
        callback.apply(null, _results);
        return null;
      },
      function(error) {
        callback(error, null);
      }).
      catch(function(error) {
        // If we made it here, we must have an error in the callback re:
        // gh-4500, so we need to emit.
        setImmediate(function() {
          _this.model.emit('error', error);
        });
      });
  }

  return promise;
};
```
<!--endsec-->


## Query#exists([path], val)

Specifies an $exists condition

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 返回值：

  * <Query> this

##### 参见：

  * [$exists](http://docs.mongodb.org/manual/reference/operator/exists/)

##### 示例：

```js

// { name: { $exists: true }}
Thing.where('name').exists()
Thing.where('name').exists(true)
Thing.find().exists('name')

// { name: { $exists: false }}
Thing.where('name').exists(false);
Thing.find().exists('name', false);
```

## Query#find([filter], [callback])

查找文档

##### 参数：

  * [filter] &lt;[Object][]&gt; mongodb selector

  * [callback] &lt;[Function][]&gt;

##### 返回值：

  <Query> this

When no callback is passed, the query is not executed. When the query is executed, the result will be an array of documents.

##### 示例：

```js
query.find({ name: 'Los Pollos Hermanos' }).find(callback)
```

<!--sec data-title="源码" data-id="Query_find" data-show=true data-collapse=true ces-->
```js
Query.prototype.find = function(conditions, callback) {
  if (typeof conditions === 'function') {
    callback = conditions;
    conditions = {};
  }

  conditions = utils.toObject(conditions);

  if (mquery.canMerge(conditions)) {
    this.merge(conditions);

    prepareDiscriminatorCriteria(this);
  } else if (conditions != null) {
    this.error(new ObjectParameterError(conditions, 'filter', 'find'));
  }

  // if we don't have a callback, then just return the query object
  if (!callback) {
    return Query.base.find.call(this);
  }

  this._find(callback);

  return this;
};

```
<!--endsec-->


## Query#findOne([filter], [projection], [options], [callback])

将查询声明为一个 findOne 操作。执行时，第一个被找到的文档被传递给回调。

##### 参数：

  * `[filter]` &lt;[Object][]&gt; mongodb selector

  * `[projection]` &lt;[Object][]&gt; optional fields to return

  * `[options]` &lt;[Object][]&gt; see setOptions()

  * `[callback]` &lt;[Function][]&gt; optional params are (error, document)

##### 返回值：

  * <Query> this

##### 参见：

  * [findOne](http://docs.mongodb.org/manual/reference/method/db.collection.findOne/)

  * [Query.select]()

Passing a callback executes the query. The result of the query is a single document.

##### 注意：
*conditions is optional, and if conditions is null or undefined, mongoose will send an empty findOne command to MongoDB, which will return an arbitrary document. If you're querying by _id, use Model.findById() instead.*

**This function triggers the following middleware**

  * findOne()


##### 示例：

```js
var query  = Kitten.where({ color: 'white' });
query.findOne(function (err, kitten) {
  if (err) return handleError(err);
  if (kitten) {
    // doc may be null if no document matched
  }
});
```
<!--sec data-title="源码" data-id="Query_findOne" data-show=true data-collapse=true ces-->
```js
Query.prototype.findOne = function(conditions, projection, options, callback) {
  if (typeof conditions === 'function') {
    callback = conditions;
    conditions = null;
    projection = null;
    options = null;
  } else if (typeof projection === 'function') {
    callback = projection;
    options = null;
    projection = null;
  } else if (typeof options === 'function') {
    callback = options;
    options = null;
  }

  // make sure we don't send in the whole Document to merge()
  conditions = utils.toObject(conditions);

  this.op = 'findOne';

  if (options) {
    this.setOptions(options);
  }

  if (projection) {
    this.select(projection);
  }

  if (mquery.canMerge(conditions)) {
    this.merge(conditions);

    prepareDiscriminatorCriteria(this);

    try {
      this.cast(this.model);
      this.error(null);
    } catch (err) {
      this.error(err);
    }
  } else if (conditions != null) {
    this.error(new ObjectParameterError(conditions, 'filter', 'findOne'));
  }

  if (!callback) {
    // already merged in the conditions, don't need to send them in.
    return Query.base.findOne.call(this);
  }

  this._findOne(callback);

  return this;
};
```
<!--endsec-->


## Query#findOneAndRemove([conditions], [options], [options.passRawResult], [options.strict], [callback])

Issues a mongodb findAndModify remove command.

##### 参数：

  * `[conditions]` &lt;[Object][]&gt;

  * `[options]` &lt;[Object][]&gt;

  * `[options.passRawResult]` &lt;[Boolean][]&gt; if true, passes the raw result from the MongoDB driver as the third callback parameter

  * `[options.strict]` <Boolean, String> overwrites the schema's strict mode option

  * `[callback]` &lt;[Function][]&gt; optional params are (error, document)

##### 返回值：

  * <Query> this

##### 参见：

  * [mongodb](http://www.mongodb.org/display/DOCS/findAndModify+Command)

Finds a matching document, removes it, passing the found document (if any) to the callback. Executes immediately if callback is passed.

**This function triggers the following middleware**

  * findOneAndRemove()


##### 可用选项

  * `sort`: if multiple docs are found by the conditions, sets the sort order to choose which doc to update
  * `maxTimeMS`: puts a time limit on the query - requires mongodb >= 2.6.0
  * `passRawResult`: if true, passes the raw result from the MongoDB driver as the third callback parameter


##### 回调函数签名

```js
function(error, doc, result) {
  // error: any errors that occurred
  // doc: the document before updates are applied if `new: false`, or after updates if `new = true`
  // result: [raw result from the MongoDB driver](http://mongodb.github.io/node-mongodb-native/2.0/api/Collection.html#findAndModify)
}
```

##### 示例：

```js
A.where().findOneAndRemove(conditions, options, callback) // executes
A.where().findOneAndRemove(conditions, options)  // return Query
A.where().findOneAndRemove(conditions, callback) // executes
A.where().findOneAndRemove(conditions) // returns Query
A.where().findOneAndRemove(callback)   // executes
A.where().findOneAndRemove()           // returns Query
```


## Query#findOneAndUpdate([query], [doc], [options], [options.passRawResult], [options.strict], [options.multipleCastError], [callback])

Issues a mongodb [findAndModify](http://www.mongodb.org/display/DOCS/findAndModify+Command) update command.

##### 参数：

  * `[query]` <Object, Query>

  * `[doc]` &lt;[Object][]&gt;

  * `[options]` &lt;[Object][]&gt;

  * `[options.passRawResult]` &lt;[Boolean][]&gt; if true, passes the [raw result from the MongoDB driver as the third callback parameter](http://mongodb.github.io/node-mongodb-native/2.0/api/Collection.html#findAndModify)

  * `[options.strict]` <Boolean, String> overwrites the schema's [strict mode option](/Library/mongoose/docs/guide.html#strict)

  * `[options.multipleCastError]` &lt;[Boolean][]&gt; by default, mongoose only returns the first error that occurred in casting the query. Turn on this option to aggregate all the cast errors.

  * `[callback]` &lt;[Function][]&gt; optional params are (error, doc), unless passRawResult is used, in which case params are (error, doc, writeOpResult)

##### 返回值：

  * <Query> this

##### 参见：

  * [mongodb](http://www.mongodb.org/display/DOCS/findAndModify+Command)

  * [writeOpResult](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#~WriteOpResult)

Finds a matching document, updates it according to the update arg, passing any options, and returns the found document (if any) to the callback. The query executes immediately if callback is passed.

**This function triggers the following middleware**

  * findOneAndUpdate()


##### 可用选项

  * `new`: bool - if true, return the modified document rather than the original. defaults to false (changed in 4.0)
  * `upsert`: bool - creates the object if it doesn't exist. defaults to false.
  * `fields`: {Object|String} - Field selection. Equivalent to .select(fields).findOneAndUpdate()
  * `sort`: if multiple docs are found by the conditions, sets the sort order to choose which doc to update
  * `maxTimeMS`: puts a time limit on the query - requires mongodb >= 2.6.0
  * `runValidators`: if true, runs update validators on this command. Update validators validate the update operation against the model's schema.
  * `setDefaultsOnInsert`: if this and upsert are true, mongoose will apply the defaults specified in the model's schema if a new document is created. This option only works on MongoDB >= 2.4 because it relies on MongoDB's $setOnInsert operator.
  * `passRawResult`: if true, passes the raw result from the MongoDB driver as the third callback parameter
  * `context` (string) if set to 'query' and runValidators is on, this will refer to the query in custom validator functions that update validation runs. Does nothing if runValidators is false.
  * `runSettersOnQuery`: bool - if true, run all setters defined on the associated model's schema for all fields defined in the query and the update.


##### 回调函数签名

```js
function(error, doc) {
  // error: any errors that occurred
  // doc: the document before updates are applied if `new: false`, or after updates if `new = true`
}
```

##### 示例：

```js
query.findOneAndUpdate(conditions, update, options, callback) // executes
query.findOneAndUpdate(conditions, update, options)  // returns Query
query.findOneAndUpdate(conditions, update, callback) // executes
query.findOneAndUpdate(conditions, update)           // returns Query
query.findOneAndUpdate(update, callback)             // returns Query
query.findOneAndUpdate(update)                       // returns Query
query.findOneAndUpdate(callback)                     // executes
query.findOneAndUpdate()                             // returns Query
```


## Query#geometry(object)

Specifies a $geometry condition

##### 参数：

  * `object` &lt;[Object][]&gt; Must contain a type property which is a String and a coordinates property which is an Array. See the examples.

##### 返回值：

  * <Query> this

##### 参见：

  * [$geometry](http://docs.mongodb.org/manual/reference/operator/geometry/)

  * http://docs.mongodb.org/manual/release-notes/2.4/#new-geospatial-indexes-with-geojson-and-improved-spherical-geometry

  * http://www.mongodb.org/display/DOCS/Geospatial+Indexing

##### 示例：

```js

var polyA = [[[ 10, 20 ], [ 10, 40 ], [ 30, 40 ], [ 30, 20 ]]]
query.where('loc').within().geometry({ type: 'Polygon', coordinates: polyA })

// or
var polyB = [[ 0, 0 ], [ 1, 1 ]]
query.where('loc').within().geometry({ type: 'LineString', coordinates: polyB })

// or
var polyC = [ 0, 0 ]
query.where('loc').within().geometry({ type: 'Point', coordinates: polyC })

// or
query.where('loc').intersects().geometry({ type: 'Point', coordinates: polyC })

```

The argument is assigned to the most recent path passed to where().

##### 注意：


geometry() must come after either intersects() or within().

The object argument must contain type and coordinates properties.

  - type {String}
  - coordinates {Array}

## Query#getQuery()

Returns the current query conditions as a JSON object.

##### 返回值：

  * &lt;[Object][]&gt; current query conditions

##### 示例：

```js
var query = new Query();
query.find({ a: 1 }).where('b').gt(2);
query.getQuery(); // { a: 1, b: { $gt: 2 } }
```

<!--sec data-title="源码" data-id="Query_getQuery" data-show=true data-collapse=true ces-->
```js
Query.prototype.getQuery = function() {
  return this._conditions;
};
```
<!--endsec-->


## Query#getUpdate()

Returns the current update operations as a JSON object.

##### 返回值：

  * &lt;[Object][]&gt; current update operations

##### 示例：

```js
var query = new Query();
query.update({}, { $set: { a: 5 } });
query.getUpdate(); // { $set: { a: 5 } }
```

<!--sec data-title="源码" data-id="Query_getUpdate" data-show=true data-collapse=true ces-->
```js
Query.prototype.getUpdate = function() {
  return this._update;
};
```
<!--endsec-->


## Query#gt([path], val)


Specifies a $gt query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 参见：

  * [$gt](http://docs.mongodb.org/manual/reference/operator/gt/)

When called with one argument, the most recent path passed to where() is used.

##### 示例：

```js
Thing.find().where('age').gt(21)

// or
Thing.find().gt('age', 21)
```


## Query#gte([path], val)


Specifies a $gte query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 参见：

  * [$gte](http://docs.mongodb.org/manual/reference/operator/gte/)

When called with one argument, the most recent path passed to where() is used.

## Query#hint(val)

Sets query hints.

##### 参数：

  * `val` &lt;[Object][]&gt; a hint object

##### 返回值：

##### 参见：

  * [$hint](http://docs.mongodb.org/manual/reference/operator/hint/)

##### 示例：

```js
query.hint({ indexA: 1, indexB: -1})
```

##### 注意：

Cannot be used with distinct()


## Query#in([path], val)

Specifies an $in query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 参见：

  [$in](http://docs.mongodb.org/manual/reference/operator/in/)

When called with one argument, the most recent path passed to where() is used.

## Query#intersects([arg])

Declares an intersects query for geometry().

##### 参数：

  * `[arg]` &lt;[Object][]&gt;

##### 返回值：

  * <Query> this

##### 参见：

  * [$geometry](http://docs.mongodb.org/manual/reference/operator/geometry/)

  * [geoIntersects](http://docs.mongodb.org/manual/reference/operator/geoIntersects/)

##### 示例：

```js
query.where('path').intersects().geometry({
    type: 'LineString'
  , coordinates: [[180.0, 11.0], [180, 9.0]]
})

query.where('path').intersects({
    type: 'LineString'
  , coordinates: [[180.0, 11.0], [180, 9.0]]
})
```

##### 注意：

**MUST** be used after where().

##### 注意：

In Mongoose 3.7, intersects changed from a getter to a function. If you need the old syntax, use this.


## Query#lean(bool)

Sets the lean option.

##### 参数：

  * `bool` <Boolean, Object> defaults to true

##### 返回值：

  * <Query> this

Documents returned from queries with the lean option enabled are plain javascript objects, not MongooseDocuments. They have no save method, getters/setters or other Mongoose magic applied.

##### 示例：

```js
new Query().lean() // true
new Query().lean(true)
new Query().lean(false)

Model.find().lean().exec(function (err, docs) {
  docs[0] instanceof mongoose.Document // false
});
```

This is a [great](https://groups.google.com/forum/#!topic/mongoose-orm/u2_DzDydcnA/discussion) option in high-performance read-only scenarios, especially when combined with stream.

<!--sec data-title="源码" data-id="Query_lean" data-show=true data-collapse=true ces-->
```js
Query.prototype.lean = function(v) {
  this._mongooseOptions.lean = arguments.length ? v : true;
  return this;
};
```
<!--endsec-->


## Query#limit(val)

Specifies the maximum number of documents the query will return.

##### 参数：

  * val <Number>

##### 示例：

```js
query.limit(20)
```

##### 注意：

Cannot be used with distinct()


## Query#lt([path], val)

Specifies a $lt query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 参见：

  * [$lt](http://docs.mongodb.org/manual/reference/operator/lt/)

When called with one argument, the most recent path passed to where() is used.


## Query#lte([path], val)

Specifies a $lte query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 参见：

  * [$lte](http://docs.mongodb.org/manual/reference/operator/lte/)

When called with one argument, the most recent path passed to where() is used.


## Query#maxDistance([path], val)

Specifies a $maxDistance query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 参见：

  * [$maxDistance](http://docs.mongodb.org/manual/reference/operator/maxDistance/)

When called with one argument, the most recent path passed to where() is used.


## Query#maxscan()

DEPRECATED Alias of maxScan

##### 参见：

  * [maxScan](http://mongoosejs.com/docs/api.html#query_Query-maxScan)



## Query#maxScan(val)]()

Specifies the maxScan option.

##### 参数：

  * `val` <Number>

##### 参见：

  * [maxScan](http://docs.mongodb.org/manual/reference/operator/maxScan/)

##### 示例：

```js
query.maxScan(100)
```

##### 注意：

Cannot be used with distinct()


## Query#merge(source)

Merges another Query or conditions object into this one.

##### 参数：

  * `source` <Query, Object>

##### 返回值：

  * <Query> this

When a Query is passed, conditions, field selection and options are merged.

<!--sec data-title="源码" data-id="Query_merge" data-show=true data-collapse=true ces-->
```js
Query.prototype.merge = function(source) {
  if (!source) {
    return this;
  }

  var opts = { retainKeyOrder: this.options.retainKeyOrder, overwrite: true };

  if (source instanceof Query) {
    // if source has a feature, apply it to ourselves

    if (source._conditions) {
      utils.merge(this._conditions, source._conditions, opts);
    }

    if (source._fields) {
      this._fields || (this._fields = {});
      utils.merge(this._fields, source._fields, opts);
    }

    if (source.options) {
      this.options || (this.options = {});
      utils.merge(this.options, source.options, opts);
    }

    if (source._update) {
      this._update || (this._update = {});
      utils.mergeClone(this._update, source._update);
    }

    if (source._distinct) {
      this._distinct = source._distinct;
    }

    return this;
  }

  // plain object
  utils.merge(this._conditions, source, opts);

  return this;
};
```
<!--endsec-->

## Query#merge(source)

Merges another Query or conditions object into this one.

##### 参数：

  * `source` <Query, Object>

##### 返回值：

  * <Query> this

When a Query is passed, conditions, field selection and options are merged.

New in 3.7.0


## Query#mod([path], val)

Specifies a $mod condition, filters documents for documents whose
path property is a number that is equal to remainder modulo divisor.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` &lt;[Array][]&gt; must be of length 2, first element is divisor, 2nd element is remainder.

##### 返回值：

  * <Query> this

##### 参见：

  * [$mod](http://docs.mongodb.org/manual/reference/operator/mod/)

##### 示例：

```js
// All find products whose inventory is odd
Product.find().mod('inventory', [2, 1]);
Product.find().where('inventory').mod([2, 1]);
// This syntax is a little strange, but supported.
Product.find().where('inventory').mod(2, 1);
```


## Query#mongooseOptions(options)

Getter/setter around the current mongoose-specific options for this query
(populate, lean, etc.)

##### 参数：

  * `options` &lt;[Object][]&gt; if specified, overwrites the current options
<!--sec data-title="源码" data-id="Query_mongooseOptions" data-show=true data-collapse=true ces-->
```js
Query.prototype.mongooseOptions = function(v) {
  if (arguments.length > 0) {
    this._mongooseOptions = v;
  }
  return this._mongooseOptions;
};
```
<!--endsec-->


## Query#ne([path], val)

Specifies a $ne query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 参见：

  * [$ne](http://docs.mongodb.org/manual/reference/operator/ne/)

When called with one argument, the most recent path passed to where() is used.


## Query#near([path], val)

Specifies a $near or $nearSphere condition

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` &lt;[Object][]&gt;

##### 返回值：

  * <Query> this

##### 参见：

  * [$near](http://docs.mongodb.org/manual/reference/operator/near/)

  * [$nearSphere](http://docs.mongodb.org/manual/reference/operator/nearSphere/)

  * [$maxDistance](http://docs.mongodb.org/manual/reference/operator/maxDistance/)

  * http://www.mongodb.org/display/DOCS/Geospatial+Indexing

These operators return documents sorted by distance.

##### 示例：

```js
query.where('loc').near({ center: [10, 10] });
query.where('loc').near({ center: [10, 10], maxDistance: 5 });
query.where('loc').near({ center: [10, 10], maxDistance: 5, spherical: true });
query.near('loc', { center: [10, 10], maxDistance: 5 });
```


## Query#nearSphere()

DEPRECATED Specifies a $nearSphere condition

##### 参见：

  * [near()]()
  * [$near](http://docs.mongodb.org/manual/reference/operator/near/)
  * [$nearSphere](http://docs.mongodb.org/manual/reference/operator/nearSphere/)
  * [$maxDistance](http://docs.mongodb.org/manual/reference/operator/maxDistance/)

##### 示例：

```js
query.where('loc').nearSphere({ center: [10, 10], maxDistance: 5 });
```

**Deprecated**. Use query.near() instead with the spherical option set to true.

##### 示例：

```js
query.where('loc').near({ center: [10, 10], spherical: true });
```

<!--sec data-title="源码" data-id="Query_nearSphere" data-show=true data-collapse=true ces-->
```js
Query.prototype.nearSphere = function() {
  this._mongooseOptions.nearSphere = true;
  this.near.apply(this, arguments);
  return this;
};
```
<!--endsec-->


## Query#nin([path], val)

Specifies an $nin query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 参见：

  * [$nin](http://docs.mongodb.org/manual/reference/operator/nin/)

When called with one argument, the most recent path passed to where() is used.


## Query#nor(array)

Specifies arguments for a $nor condition.

##### 参数：

  * `array` &lt;[Array][]&gt; array of conditions

##### 返回值：

  * <Query> this

##### 参见：

  * [$nor](http://docs.mongodb.org/manual/reference/operator/nor/)

##### 示例：

```js
query.nor([{ color: 'green' }, { status: 'ok' }])
```


## Query#or(array)

Specifies arguments for an $or condition.

##### 参数：

  * `array` &lt;[Array][]&gt; array of conditions

##### 返回值：

  * <Query> this

##### 参见：

  * [$or](http://docs.mongodb.org/manual/reference/operator/or/)

##### 示例：

```js
query.or([{ color: 'red' }, { status: 'emergency' }])
```


## Query#polygon([path], [coordinatePairs...])

Specifies a $polygon condition


##### 参数：

  * `[path]` <String, Array>

  * `[coordinatePairs...]` <Array, Object>

##### 返回值：

  * <Query> this

##### 参见：

  * [$polygon](http://docs.mongodb.org/manual/reference/operator/polygon/)

  * http://www.mongodb.org/display/DOCS/Geospatial+Indexing

##### 示例：

```js
query.where('loc').within().polygon([10,20], [13, 25], [7,15])
query.polygon('loc', [10,20], [13, 25], [7,15])
```


## Query#populate(path, [select], [model], [match], [options])

Specifies paths which should be populated with other documents.

##### 参数：

  * `path` <Object, String> either the path to populate or an object specifying all parameters

  * `[select]` <Object, String> Field selection for the population query

  * `[model]` <Model> The model you wish to use for population. If not specified, populate will look up the model by the name in the Schema's ref field.

  * `[match]` &lt;[Object][]&gt; Conditions for the population query

  * `[options]` &lt;[Object][]&gt; Options for the population query (sort, etc)

##### 返回值：

  * <Query> this

##### 参见：

  * [population](/Library/mongoose/docs/populate.md)

  * [Query#select]()

  * [Model.populate]()

##### 示例：

```js
Kitten.findOne().populate('owner').exec(function (err, kitten) {
  console.log(kitten.owner.name) // Max
})

Kitten.find().populate({
    path: 'owner'
  , select: 'name'
  , match: { color: 'black' }
  , options: { sort: { name: -1 }}
}).exec(function (err, kittens) {
  console.log(kittens[0].owner.name) // Zoopa
})

// alternatively
Kitten.find().populate('owner', 'name', null, {sort: { name: -1 }}).exec(function (err, kittens) {
  console.log(kittens[0].owner.name) // Zoopa
})
```

Paths are populated after the query executes and a response is received. A separate query is then executed for each path specified for population. After a response for each query has also been returned, the results are passed to the callback.

<!--sec data-title="源码" data-id="Query_populate" data-show=true data-collapse=true ces-->
```js
Query.prototype.populate = function() {
  if (arguments.length === 0) {
    return this;
  }

  var i;

  var res = utils.populate.apply(null, arguments);

  // Propagate readPreference from parent query, unless one already specified
  if (this.options && this.options.readPreference != null) {
    for (i = 0; i < res.length; ++i) {
      if (!res[i].options || res[i].options.readPreference == null) {
        res[i].options = res[i].options || {};
        res[i].options.readPreference = this.options.readPreference;
      }
    }
  }

  var opts = this._mongooseOptions;

  if (!utils.isObject(opts.populate)) {
    opts.populate = {};
  }

  var pop = opts.populate;

  for (i = 0; i < res.length; ++i) {
    var path = res[i].path;
    if (pop[path] && pop[path].populate && res[i].populate) {
      res[i].populate = pop[path].populate.concat(res[i].populate);
    }
    pop[res[i].path] = res[i];
  }

  return this;
};
```
<!--endsec-->


## Query#read(pref, [tags])

Determines the MongoDB nodes from which to read.

##### 参数：

  * `pref` &lt;[String][]&gt; one of the listed preference options or aliases

  * `[tags]` &lt;[Array][]&gt; optional tags for this query

##### 返回值：

  * <Query> this

##### 参见：

  * [mongodb](http://docs.mongodb.org/manual/applications/replication/#read-preference)

  * [driver](http://mongodb.github.com/node-mongodb-native/driver-articles/anintroductionto1_1and2_2.html#read-preferences)

##### 引用:

```
primary - (default) Read from primary only. Operations will produce an error if primary is unavailable. Cannot be combined with tags.
secondary            Read from secondary if available, otherwise error.
primaryPreferred     Read from primary if available, otherwise a secondary.
secondaryPreferred   Read from a secondary if available, otherwise read from the primary.
nearest              All operations read from among the nearest candidates, but unlike other modes, this option will include both the primary and all secondaries in the random selection.
```

别名：

```
p   primary
pp  primaryPreferred
s   secondary
sp  secondaryPreferred
n   nearest
```
##### 示例：

```js
new Query().read('primary')
new Query().read('p')  // same as primary

new Query().read('primaryPreferred')
new Query().read('pp') // same as primaryPreferred

new Query().read('secondary')
new Query().read('s')  // same as secondary

new Query().read('secondaryPreferred')
new Query().read('sp') // same as secondaryPreferred

new Query().read('nearest')
new Query().read('n')  // same as nearest

// read from secondaries with matching tags
new Query().read('s', [{ dc:'sf', s: 1 },{ dc:'ma', s: 2 }])
```

Read more about how to use read preferrences here and here.


## Query#regex([path], val)

Specifies a $regex query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <String, RegExp>

##### 参见：

  * [$regex](http://docs.mongodb.org/manual/reference/operator/regex/)

When called with one argument, the most recent path passed to where() is used.


## Query#remove([filter], [callback])

Declare and/or execute this query as a remove() operation.

##### 参数：

  * `[filter]` <Object, Query> mongodb selector

  * `[callback]` &lt;[Function][]&gt; optional params are (error, writeOpResult)

##### 返回值：

  * <Query> this

##### 参见：

  * [writeOpResult](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#~WriteOpResult)

  * [remove](http://docs.mongodb.org/manual/reference/method/db.collection.remove/)

This function does not trigger any middleware

##### 示例：

```js
Model.remove({ artist: 'Anne Murray' }, callback)
```

##### 注意：

The operation is only executed when a callback is passed. To force execution without a callback, you must first call remove() and then execute it by using the exec() method.

```js
// not executed
var query = Model.find().remove({ name: 'Anne Murray' })

// executed
query.remove({ name: 'Anne Murray' }, callback)
query.remove({ name: 'Anne Murray' }).remove(callback)

// executed without a callback
query.exec()

// summary
query.remove(conds, fn); // executes
query.remove(conds)
query.remove(fn) // executes
query.remove()
```

<!--sec data-title="源码" data-id="Query_remove" data-show=true data-collapse=true ces-->
```js
Query.prototype.remove = function(filter, callback) {
  if (typeof filter === 'function') {
    callback = filter;
    filter = null;
  }

  filter = utils.toObject(filter, { retainKeyOrder: true });

  try {
    this.cast(this.model, filter);
    this.merge(filter);
  } catch (err) {
    this.error(err);
  }

  prepareDiscriminatorCriteria(this);

  if (!callback) {
    return Query.base.remove.call(this);
  }

  return this._remove(callback);
};

```
<!--endsec-->


## Query#replaceOne([criteria], [doc], [options], [callback])

Declare and/or execute this query as a replaceOne() operation. Same as
update(), except MongoDB will replace the existing document and will
not accept any atomic operators ($set, etc.)

##### 参数：

  * `[criteria]` &lt;[Object][]&gt;

  * `[doc]` &lt;[Object][]&gt; the update command

  * `[options]` &lt;[Object][]&gt;

  * `[callback]` &lt;[Function][]&gt; optional params are (error, writeOpResult)

##### 返回值：

  * <Query> this

##### 参见：

  * [Model.update](http://mongoosejs.com/docs/api.html#model_Model.update)

  * [update](http://docs.mongodb.org/manual/reference/method/db.collection.update/)

  * [writeOpResult](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#~WriteOpResult)

##### 注意：

replaceOne will not fire update middleware. Use pre('replaceOne')
and post('replaceOne') instead.

**This function triggers the following middleware**

  * replaceOne()


<!--sec data-title="源码" data-id="Query_replaceOne" data-show=true data-collapse=true ces-->
```js
Query.prototype.replaceOne = function(conditions, doc, options, callback) {
  if (typeof options === 'function') {
    // .update(conditions, doc, callback)
    callback = options;
    options = null;
  } else if (typeof doc === 'function') {
    // .update(doc, callback);
    callback = doc;
    doc = conditions;
    conditions = {};
    options = null;
  } else if (typeof conditions === 'function') {
    // .update(callback)
    callback = conditions;
    conditions = undefined;
    doc = undefined;
    options = undefined;
  } else if (typeof conditions === 'object' && !doc && !options && !callback) {
    // .update(doc)
    doc = conditions;
    conditions = undefined;
    options = undefined;
    callback = undefined;
  }

  this.setOptions({ overwrite: true });
  return _update(this, 'replaceOne', conditions, doc, options, callback);
};
```
<!--endsec-->


## Query#select(arg)

Specifies which document fields to include or exclude (also known as the query "projection")

##### 参数：

  * `arg` <Object, String>

##### 返回值：

  * <Query> this

##### 参见：

  * [SchemaType]()

When using string syntax, prefixing a path with - will flag that path as excluded. When a path does not have the - prefix, it is included. Lastly, if a path is prefixed with +, it forces inclusion of the path, which is useful for paths excluded at the [schema level](http://mongoosejs.com/docs/api.html#schematype_SchemaType-select).

A projection must be either inclusive or exclusive. In other words, you must
either list the fields to include (which excludes all others), or list the fields
to exclude (which implies all other fields are included). The [_id field is the only exception because MongoDB includes it by default.](https://docs.mongodb.com/manual/tutorial/project-fields-from-query-results/#suppress-id-field)

##### 示例：

```js
// include a and b, exclude other fields
query.select('a b');

// exclude c and d, include other fields
query.select('-c -d');

// or you may use object notation, useful when
// you have keys already prefixed with a "-"
query.select({ a: 1, b: 1 });
query.select({ c: 0, d: 0 });

// force inclusion of field excluded at schema level
query.select('+path')
```


## Query#selected()

Determines if field selection has been made.

##### 返回值：

  * &lt;[Boolean][]&gt;



## Query#selectedExclusively()

Determines if exclusive field selection has been made.

##### 返回值：

  * &lt;[Boolean][]&gt;

```js
query.selectedExclusively() // false
query.select('-name')
query.selectedExclusively() // true
query.selectedInclusively() // false
```


## Query#selectedInclusively()

Determines if inclusive field selection has been made.

##### 返回值：

  * &lt;[Boolean][]&gt;

```js
query.selectedInclusively() // false
query.select('name')
query.selectedInclusively() // true
```


## Query#setOptions(options)

Sets query options. Some options only make sense for certain operations.

##### 参数：

  * `options` &lt;[Object][]&gt;

##### 选项：

The following options are only for find():

  - [tailable](http://www.mongodb.org/display/DOCS/Tailable+Cursors)
  - [sort](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries-%7B%7Bsort()%7D%7D)
  - [limit](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries-%7B%7Blimit%28%29%7D%7D)
  - [skip](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries-%7B%7Bskip%28%29%7D%7D)
  - [maxscan](https://docs.mongodb.org/v3.2/reference/operator/meta/maxScan/#metaOp._S_maxScan)
  - [batchSize](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries-%7B%7BbatchSize%28%29%7D%7D)
  - [comment](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries-%24comment)
  - [snapshot](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries-%7B%7Bsnapshot%28%29%7D%7D)
  - [readPreference](http://docs.mongodb.org/manual/applications/replication/#read-preference)
  - [hint](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries-%24hint)

The following options are only for update(), updateOne(), updateMany(), replaceOne(), and findOneAndUpdate():
  - [upsert](https://docs.mongodb.com/manual/reference/method/db.collection.update/)
  - [writeConcern](https://docs.mongodb.com/manual/reference/method/db.collection.update/)

The following options are only for find(), findOne(), findById(), and findOneAndUpdate():
  - [lean](http://mongoosejs.com/docs/api.html#query_Query-lean)

**The following options are for all operations**

  * [collation](https://docs.mongodb.com/manual/reference/collation/)


<!--sec data-title="源码" data-id="Query_setOptions" data-show=true data-collapse=true ces-->
```js
Query.prototype.setOptions = function(options, overwrite) {
  // overwrite is only for internal use
  if (overwrite) {
    // ensure that _mongooseOptions & options are two different objects
    this._mongooseOptions = (options && utils.clone(options)) || {};
    this.options = options || {};

    if ('populate' in options) {
      this.populate(this._mongooseOptions);
    }
    return this;
  }

  if (options == null) {
    return this;
  }

  if (Array.isArray(options.populate)) {
    var populate = options.populate;
    delete options.populate;
    var _numPopulate = populate.length;
    for (var i = 0; i < _numPopulate; ++i) {
      this.populate(populate[i]);
    }
  }

  return Query.base.setOptions.call(this, options);
};
```
<!--endsec-->


## Query#size([path], val)

Specifies a $size query condition.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number>

##### 参见：

  * [$size](http://docs.mongodb.org/manual/reference/operator/size/)

When called with one argument, the most recent path passed to where() is used.

##### 示例：

```js
MyModel.where('tags').size(0).exec(function (err, docs) {
  if (err) return handleError(err);

  assert(Array.isArray(docs));
  console.log('documents with 0 tags', docs);
})
```


## Query#skip(val)

Specifies the number of documents to skip.

##### 参数：

  * `val` <Number>

##### 参见：

  * [cursor.skip](http://docs.mongodb.org/manual/reference/method/cursor.skip/)

##### 示例：

```js
query.skip(100).limit(20)
```

##### 注意：

Cannot be used with distinct()



## Query#slaveOk(v)

DEPRECATED Sets the slaveOk option.

##### 参数：

  * `v` &lt;[Boolean][]&gt; defaults to true

##### 返回值：

  * <Query> this

##### 参见：

  * [mongodb](http://docs.mongodb.org/manual/applications/replication/#read-preference)

  * [slaveOk](http://docs.mongodb.org/manual/reference/method/rs.slaveOk/)

  * [read()]()

Deprecated in MongoDB 2.2 in favor of read preferences.

##### 示例：

```js
query.slaveOk() // true
query.slaveOk(true)
query.slaveOk(false)
```


## Query#slice([path], val)

Specifies a $slice projection for an array.

##### 参数：

  * `[path]` &lt;[String][]&gt;

  * `val` <Number> number/range of elements to slice

##### 返回值：

  * <Query> this

##### 参见：

  * [mongodb](http://www.mongodb.org/display/DOCS/Retrieving+a+Subset+of+Fields#RetrievingaSubsetofFields-RetrievingaSubrangeofArrayElements)

  * [$slice](http://docs.mongodb.org/manual/reference/projection/slice/#prj._S_slice)

##### 示例：

```js
query.slice('comments', 5)
query.slice('comments', -5)
query.slice('comments', [10, 5])
query.where('comments').slice(5)
query.where('comments').slice([-10, 5])
```


## Query#slice([path], [val])

Specifies a path for use with chaining.

##### 参数：

  * `[path]` <String, Object>

  * `[val]` <T>

##### 返回值：

  * <Query> this

##### 示例：

```js
// instead of writing:
User.find({age: {$gte: 21, $lte: 65}}, callback);

// we can instead write:
User.where('age').gte(21).lte(65);

// passing query conditions is permitted
User.find().where({ name: 'vonderful' })

// chaining
User
.where('age').gte(21).lte(65)
.where('name', /^vonderful/i)
.where('friends').slice(10)
.exec(callback)
```


## Query#snapshot()

Specifies this query as a snapshot query.

##### 返回值：

  * <Query> this

##### 参见：

  * [snapshot](http://docs.mongodb.org/manual/reference/operator/snapshot/)

##### 示例：

```js
query.snapshot() // true
query.snapshot(true)
query.snapshot(false)
```
##### 注意：

Cannot be used with distinct()


## Query#sort(arg)

Sets the sort order

##### 参数：

  * `arg` <Object, String>

##### 返回值：

  * <Query> this

##### 参见：

  * [cursor.sort](http://docs.mongodb.org/manual/reference/method/cursor.sort/)

If an object is passed, values allowed are asc, desc, ascending, descending, 1, and -1.

If a string is passed, it must be a space delimited list of path names. The
sort order of each path is ascending unless the path name is prefixed with -
which will be treated as descending.

##### 示例：

```js
// sort by "field" ascending and "test" descending
query.sort({ field: 'asc', test: -1 });

// equivalent
query.sort('field -test');
```

##### 注意：

Cannot be used with distinct()

<!--sec data-title="源码" data-id="Query_sort" data-show=true data-collapse=true ces-->
```js
Query.prototype.sort = function(arg) {
  if (arguments.length > 1) {
    throw new Error('sort() only takes 1 Argument');
  }

  return Query.base.sort.call(this, arg);
};
```
<!--endsec-->


## Query#stream([options])

Returns a Node.js 0.8 style read stream interface.

##### 参数：

  * `[options]` &lt;[Object][]&gt;

##### 返回值：

  * <QueryStream>

##### 参见：

  * [QueryStream]()

##### 示例：

```js
// follows the nodejs 0.8 stream api
Thing.find({ name: /^hello/ }).stream().pipe(res)

// manual streaming
var stream = Thing.find({ name: /^hello/ }).stream();

stream.on('data', function (doc) {
  // do something with the mongoose document
}).on('error', function (err) {
  // handle the error
}).on('close', function () {
  // the stream is closed
});
```

##### 可用选项

  * `transform`: optional function which accepts a mongoose document. The return value of the function will be emitted on data.


##### 示例：

```js
// JSON.stringify all documents before emitting
var stream = Thing.find().stream({ transform: JSON.stringify });
stream.pipe(writeStream);
```

<!--sec data-title="源码" data-id="Query_stream" data-show=true data-collapse=true ces-->
```js
Query.prototype.stream = function stream(opts) {
  this._applyPaths();
  this._fields = this._castFields(this._fields);
  this._castConditions();
  return new QueryStream(this, opts);
};
Query.prototype.stream = util.deprecate(Query.prototype.stream, 'Mongoose: ' +
  'Query.prototype.stream() is deprecated in mongoose >= 4.5.0, ' +
  'use Query.prototype.cursor() instead');
```
<!--endsec-->


## Query#tailable(bool, [opts], [opts.numberOfRetries], [opts.tailableRetryInterval])

Sets the tailable option (for use with capped collections).

##### 参数：

  * `bool` &lt;[Boolean][]&gt; defaults to true

  * `[opts]` &lt;[Object][]&gt; options to set

  * `[opts.numberOfRetries]` <Number> if cursor is exhausted, retry this many times before giving up

  * `[opts.tailableRetryInterval]` <Number> if cursor is exhausted, wait this many milliseconds before
 retrying

##### 参见：

  * [tailable](http://docs.mongodb.org/manual/tutorial/create-tailable-cursor/)

##### 示例：

```js
query.tailable() // true
query.tailable(true)
query.tailable(false)
```

##### 注意：

Cannot be used with distinct()

<!--sec data-title="源码" data-id="Query_tailable" data-show=true data-collapse=true ces-->
```js
Query.prototype.tailable = function(val, opts) {
  // we need to support the tailable({ awaitdata : true }) as well as the
  // tailable(true, {awaitdata :true}) syntax that mquery does not support
  if (val && val.constructor.name === 'Object') {
    opts = val;
    val = true;
  }

  if (val === undefined) {
    val = true;
  }

  if (opts && typeof opts === 'object') {
    for (var key in opts) {
      if (key === 'awaitdata') {
        // For backwards compatibility
        this.options[key] = !!opts[key];
      } else {
        this.options[key] = opts[key];
      }
    }
  }

  return Query.base.tailable.call(this, val);
};
```
<!--endsec-->


## Query#then([resolve], [reject])

Executes the query returning a Promise which will be
resolved with either the doc(s) or rejected with the error.

##### 参数：

  * `[resolve]` &lt;[Function][]&gt;

  * `[reject]` &lt;[Function][]&gt;

##### 返回值：

  * <Promise>

<!--sec data-title="源码" data-id="Query_then" data-show=true data-collapse=true ces-->
```js
Query.prototype.then = function(resolve, reject) {
  return this.exec().then(resolve, reject);
};
```
<!--endsec-->


## Query#toConstructor()

Converts this query to a customized, reusable query constructor with all arguments and options retained.

##### 返回值：

  * <Query> subclass-of-Query

##### 示例：

```js
// Create a query for adventure movies and read from the primary
// node in the replica-set unless it is down, in which case we'll
// read from a secondary node.
var query = Movie.find({ tags: 'adventure' }).read('primaryPreferred');

// create a custom Query constructor based off these settings
var Adventure = query.toConstructor();

// Adventure is now a subclass of mongoose.Query and works the same way but with the
// default query parameters and options set.
Adventure().exec(callback)

// further narrow down our query results while still using the previous settings
Adventure().where({ name: /^Life/ }).exec(callback);

// since Adventure is a stand-alone constructor we can also add our own
// helper methods and getters without impacting global queries
Adventure.prototype.startsWith = function (prefix) {
  this.where({ name: new RegExp('^' + prefix) })
  return this;
}
Object.defineProperty(Adventure.prototype, 'highlyRated', {
  get: function () {
    this.where({ rating: { $gt: 4.5 }});
    return this;
  }
})
Adventure().highlyRated.startsWith('Life').exec(callback)
```

New in 3.7.3

<!--sec data-title="源码" data-id="Query_toConstructor" data-show=true data-collapse=true ces-->
```js
Query.prototype.toConstructor = function toConstructor() {
  var model = this.model;
  var coll = this.mongooseCollection;

  var CustomQuery = function(criteria, options) {
    if (!(this instanceof CustomQuery)) {
      return new CustomQuery(criteria, options);
    }
    this._mongooseOptions = utils.clone(p._mongooseOptions);
    Query.call(this, criteria, options || null, model, coll);
  };

  util.inherits(CustomQuery, Query);

  // set inherited defaults
  var p = CustomQuery.prototype;

  p.options = {};

  p.setOptions(this.options);

  p.op = this.op;
  p._conditions = utils.clone(this._conditions, { retainKeyOrder: true });
  p._fields = utils.clone(this._fields);
  p._update = utils.clone(this._update, {
    flattenDecimals: false,
    retainKeyOrder: true
  });
  p._path = this._path;
  p._distinct = this._distinct;
  p._collection = this._collection;
  p._mongooseOptions = this._mongooseOptions;

  return CustomQuery;
};
```
<!--endsec-->


## Query#update([criteria], [doc], [options], [options.multipleCastError], [callback])

Declare and/or execute this query as an update() operation.

##### 参数：

  * `[criteria]` &lt;[Object][]&gt;

  * `[doc]` &lt;[Object][]&gt; the update command

  * `[options]` &lt;[Object][]&gt;

  * `[options.multipleCastError]` &lt;[Boolean][]&gt; by default, mongoose only returns the first error that occurred in casting the query. Turn on this option to aggregate all the cast errors.

  * `[callback]` &lt;[Function][]&gt; optional, params are (error, writeOpResult)

##### 返回值：

  * <Query> this

##### 参见：

  * [Model.update]()

  * [update](http://docs.mongodb.org/manual/reference/method/db.collection.update/)

  * [writeOpResult](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#~WriteOpResult)

All paths passed that are not $atomic operations will become $set ops.

This function triggers the following middleware

  * update()

##### 示例：

```js
Model.where({ _id: id }).update({ title: 'words' })

// becomes

Model.where({ _id: id }).update({ $set: { title: 'words' }})
```

##### 可用选项:

  * `safe` (boolean) safe mode (defaults to value set in schema (true))
  * `upsert` (boolean) whether to create the doc if it doesn't match (false)
  * `multi` (boolean) whether multiple documents should be updated (false)
  * `runValidators`: if true, runs update validators on this command. Update validators validate the update operation against the model's schema.
  * `setDefaultsOnInsert`: if this and upsert are true, mongoose will apply the defaults specified in the model's schema if a new document is created. This option only works on MongoDB >= 2.4 because it relies on MongoDB's $setOnInsert operator.
  * `strict` (boolean) overrides the strict option for this update
  * `overwrite` (boolean) disables update-only mode, allowing you to overwrite the doc (false)
  * `context` (string) if set to 'query' and runValidators is on, this will refer to the query in custom validator functions that update validation runs. Does nothing if runValidators is false.

##### 注意：

Passing an empty object {} as the doc will result in a no-op unless the overwrite option is passed. Without the overwrite option set, the update operation will be ignored and the callback executed without sending the command to MongoDB so as to prevent accidently overwritting documents in the collection.

##### 注意：

The operation is only executed when a callback is passed. To force execution without a callback, we must first call update() and then execute it by using the exec() method.

```js
var q = Model.where({ _id: id });
q.update({ $set: { name: 'bob' }}).update(); // not executed

q.update({ $set: { name: 'bob' }}).exec(); // executed

// keys that are not $atomic ops become $set.
// this executes the same command as the previous example.
q.update({ name: 'bob' }).exec();

// overwriting with empty docs
var q = Model.where({ _id: id }).setOptions({ overwrite: true })
q.update({ }, callback); // executes

// multi update with overwrite to empty doc
var q = Model.where({ _id: id });
q.setOptions({ multi: true, overwrite: true })
q.update({ });
q.update(callback); // executed

// multi updates
Model.where()
     .update({ name: /^match/ }, { $set: { arr: [] }}, { multi: true }, callback)

// more multi updates
Model.where()
     .setOptions({ multi: true })
     .update({ $set: { arr: [] }}, callback)

// single update by default
Model.where({ email: 'address@example.com' })
     .update({ $inc: { counter: 1 }}, callback)
```

API 总结

```js
update(criteria, doc, options, cb) // executes
update(criteria, doc, options)
update(criteria, doc, cb) // executes
update(criteria, doc)
update(doc, cb) // executes
update(doc)
update(cb) // executes
update(true) // executes
update()
```

<!--sec data-title="源码" data-id="Query_update" data-show=true data-collapse=true ces-->
```js
Query.prototype.update = function(conditions, doc, options, callback) {
  if (typeof options === 'function') {
    // .update(conditions, doc, callback)
    callback = options;
    options = null;
  } else if (typeof doc === 'function') {
    // .update(doc, callback);
    callback = doc;
    doc = conditions;
    conditions = {};
    options = null;
  } else if (typeof conditions === 'function') {
    // .update(callback)
    callback = conditions;
    conditions = undefined;
    doc = undefined;
    options = undefined;
  } else if (typeof conditions === 'object' && !doc && !options && !callback) {
    // .update(doc)
    doc = conditions;
    conditions = undefined;
    options = undefined;
    callback = undefined;
  }

  return _update(this, 'update', conditions, doc, options, callback);
};

```
<!--endsec-->


## Query#updateMany([criteria], [doc], [options], [callback])

Declare and/or execute this query as an updateMany() operation. Same as
update(), except MongoDB will update all documents that match
criteria (as opposed to just the first one) regardless of the value of
the multi option.

##### 参数：

  * `[criteria]` &lt;[Object][]&gt;

  * `[doc]` &lt;[Object][]&gt; the update command

  * `[options]` &lt;[Object][]&gt;

  * `[callback]` &lt;[Function][]&gt; optional params are (error, writeOpResult)

##### 返回值：

  * <Query> this

##### 参见：

  * [Model.update]()

  * [update](http://docs.mongodb.org/manual/reference/method/db.collection.update/)

  * [writeOpResult](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#~WriteOpResult)

##### 注意：

 updateMany will not fire update middleware. Use pre('updateMany')
and post('updateMany') instead.

**This function triggers the following middleware**

  * updateMany()
<!--sec data-title="源码" data-id="Query_updateMany" data-show=true data-collapse=true ces-->
```js
Query.prototype.updateMany = function(conditions, doc, options, callback) {
  if (typeof options === 'function') {
    // .update(conditions, doc, callback)
    callback = options;
    options = null;
  } else if (typeof doc === 'function') {
    // .update(doc, callback);
    callback = doc;
    doc = conditions;
    conditions = {};
    options = null;
  } else if (typeof conditions === 'function') {
    // .update(callback)
    callback = conditions;
    conditions = undefined;
    doc = undefined;
    options = undefined;
  } else if (typeof conditions === 'object' && !doc && !options && !callback) {
    // .update(doc)
    doc = conditions;
    conditions = undefined;
    options = undefined;
    callback = undefined;
  }

  return _update(this, 'updateMany', conditions, doc, options, callback);
};
```
<!--endsec-->



## Query#updateOne([criteria], [doc], [options], [callback])

Declare and/or execute this query as an updateOne() operation. Same as
update(), except MongoDB will update only the first document that
matches criteria regardless of the value of the multi option.

##### 参数：

  * `[criteria]` &lt;[Object][]&gt;

  * `[doc]` &lt;[Object][]&gt; the update command

  * `[options]` &lt;[Object][]&gt;

  * `[callback]` &lt;[Function][]&gt; params are (error, writeOpResult)

##### 返回值：

  * <Query> this

##### 参见：

  * [Model.update]()

  * [update](http://docs.mongodb.org/manual/reference/method/db.collection.update/)

  * [writeOpResult](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#~WriteOpResult)

##### 注意：

 updateOne will not fire update middleware. Use pre('updateOne')
and post('updateOne') instead.

**This function triggers the following middleware**

  * updateOne()
<!--sec data-title="源码" data-id="Query_updateOne" data-show=true data-collapse=true ces-->
```js
Query.prototype.updateOne = function(conditions, doc, options, callback) {
  if (typeof options === 'function') {
    // .update(conditions, doc, callback)
    callback = options;
    options = null;
  } else if (typeof doc === 'function') {
    // .update(doc, callback);
    callback = doc;
    doc = conditions;
    conditions = {};
    options = null;
  } else if (typeof conditions === 'function') {
    // .update(callback)
    callback = conditions;
    conditions = undefined;
    doc = undefined;
    options = undefined;
  } else if (typeof conditions === 'object' && !doc && !options && !callback) {
    // .update(doc)
    doc = conditions;
    conditions = undefined;
    options = undefined;
    callback = undefined;
  }

  return _update(this, 'updateOne', conditions, doc, options, callback);
};
```
<!--endsec-->


## Query#within()

Defines a $within or $geoWithin argument for geo-spatial queries.

##### 返回值：

  * <Query> this

##### 参见：

  * [$polygon](http://docs.mongodb.org/manual/reference/operator/polygon/)

  * [$box](http://docs.mongodb.org/manual/reference/operator/box/)

  * [$geometry](http://docs.mongodb.org/manual/reference/operator/geometry/)

  * [$center](http://docs.mongodb.org/manual/reference/operator/center/)

  * [$centerSphere](http://docs.mongodb.org/manual/reference/operator/centerSphere/)

##### 示例：

```js
query.where(path).within().box()
query.where(path).within().circle()
query.where(path).within().geometry()

query.where('loc').within({ center: [50,50], radius: 10, unique: true, spherical: true });
query.where('loc').within({ box: [[40.73, -73.9], [40.7, -73.988]] });
query.where('loc').within({ polygon: [[],[],[],[]] });

query.where('loc').within([], [], []) // polygon
query.where('loc').within([], []) // box
query.where('loc').within({ type: 'LineString', coordinates: [...] }); // geometry
```

**MUST** be used after where().

##### 注意：

As of Mongoose 3.7, $geoWithin is always used for queries. To change this behavior, see Query.use$geoWithin.

##### 注意：

In Mongoose 3.7, within changed from a getter to a function. If you need the old syntax, use this.




## Query#use$geoWithin

Flag to opt out of using $geoWithin.

```js
mongoose.Query.use$geoWithin = false;
```

MongoDB 2.4 deprecated the use of $within, replacing it with $geoWithin. Mongoose uses $geoWithin by default (which is 100% backward compatible with $within). If you are running an older version of MongoDB, set this flag to false so your within() queries continue to work.

<!--sec data-title="源码" data-id="Query_use_geoWithin" data-show=true data-collapse=true ces-->
```js
Query.use$geoWithin = mquery.use$geoWithin;
```
<!--endsec-->
##### 参见：

http://docs.mongodb.org/manual/reference/operator/geoWithin/


----


# aggregate.js

> 源码：[aggregate.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/aggregate.js)


## Aggregate#addCursorFlag(flag, value)

Adds a cursor flag

##### 参数：

  * flag &lt;[String][]&gt;

  * value &lt;[Boolean][]&gt;

##### 参见：

  * [mongodb](http://mongodb.github.io/node-mongodb-native/2.2/api/Cursor.html#addCursorFlag)

##### 示例：

```js
Model.aggregate(..).addCursorFlag('noCursorTimeout', true).exec();
```

<!--sec data-title="源码" data-id="Aggregate_addCursorFlag" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.addCursorFlag = function(flag, value) {
  if (!this.options) {
    this.options = {};
  }
  this.options[flag] = value;
  return this;
};
```
<!--endsec-->


## Aggregate#addFields(arg)

Appends a new $addFields operator to this aggregate pipeline.
Requires MongoDB v3.4+ to work

##### 参数：

  * `arg` &lt;[Object][]&gt; field specification

##### 返回值：

  * <Aggregate>

##### 参见：

  * [$addFields](https://docs.mongodb.com/manual/reference/operator/aggregation/addFields/)

##### 示例：

```js
// adding new fields based on existing fields
aggregate.addFields({
    newField: '$b.nested'
  , plusTen: { $add: ['$val', 10]}
  , sub: {
       name: '$a'
    }
})

// etc
aggregate.addFields({ salary_k: { $divide: [ "$salary", 1000 ] } });
```

<!--sec data-title="源码" data-id="Aggregate_addFields" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.addFields = function(arg) {
  var fields = {};
  if (typeof arg === 'object' && !util.isArray(arg)) {
    Object.keys(arg).forEach(function(field) {
      fields[field] = arg[field];
    });
  } else {
    throw new Error('Invalid addFields() argument. Must be an object');
  }
  return this.append({$addFields: fields});
};
```
<!--endsec-->


## Aggregate([ops])

Aggregate constructor used for building aggregation pipelines.

##### 参数：

  * `[ops]` <Object, Array> aggregation operator(s) or operator array

##### 参见：

  * [MongoDB](http://docs.mongodb.org/manual/applications/aggregation/)

  * [driver](http://mongodb.github.com/node-mongodb-native/api-generated/collection.html#aggregate)

##### 示例：

```js
new Aggregate();
new Aggregate({ $project: { a: 1, b: 1 } });
new Aggregate({ $project: { a: 1, b: 1 } }, { $skip: 5 });
new Aggregate([{ $project: { a: 1, b: 1 } }, { $skip: 5 }]);
```

Returned when calling Model.aggregate().

##### 示例：

```js
Model
.aggregate({ $match: { age: { $gte: 21 }}})
.unwind('tags')
.exec(callback)
```

##### 注意：

  * The documents returned are plain javascript objects, not mongoose documents (since any shape of document can be returned).
  * Requires MongoDB >= 2.1
  * Mongoose does not cast pipeline stages. new Aggregate({ $match: { _id: '00000000000000000000000a' } }); will not work unless _id is a string in the database. Use new Aggregate({ $match: { _id: mongoose.Types.ObjectId('00000000000000000000000a') } }); instead.


<!--sec data-title="源码" data-id="aggregate" data-show=true data-collapse=true ces-->
```js
function Aggregate() {
  this._pipeline = [];
  this._model = undefined;
  this.options = {};

  if (arguments.length === 1 && util.isArray(arguments[0])) {
    this.append.apply(this, arguments[0]);
  } else {
    this.append.apply(this, arguments);
  }
}
```
<!--endsec-->


## Aggregate#allowDiskUse(value, [tags])

Sets the allowDiskUse option for the aggregation query (ignored for < 2.6.0)

##### 参数：

  * `value` &lt;[Boolean][]&gt; Should tell server it can use hard drive to store data during aggregation.

  * `[tags]` &lt;[Array][]&gt; optional tags for this query

##### 参见：

  * [mongodb](http://docs.mongodb.org/manual/reference/command/aggregate/)

##### 示例：

```js
Model.aggregate(..).allowDiskUse(true).exec(callback)
```

<!--sec data-title="源码" data-id="Aggregate_allowDiskUse" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.allowDiskUse = function(value) {
  this.options.allowDiskUse = value;
  return this;
};
```
<!--endsec-->


## Aggregate#append(ops)

Appends new operators to this aggregate pipeline

##### 参数：

  * `ops` &lt;[Object][]&gt; operator(s) to append

##### 返回值：

  * <Aggregate>

##### 示例：

```js
aggregate.append({ $project: { field: 1 }}, { $limit: 2 });

// or pass an array
var pipeline = [{ $match: { daw: 'Logic Audio X' }} ];
aggregate.append(pipeline);
```

<!--sec data-title="源码" data-id="Aggregate_append" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.append = function() {
  var args = (arguments.length === 1 && util.isArray(arguments[0]))
      ? arguments[0]
      : utils.args(arguments);

  if (!args.every(isOperator)) {
    throw new Error('Arguments must be aggregate pipeline operators');
  }

  this._pipeline = this._pipeline.concat(args);

  return this;
};
```
<!--endsec-->


## Aggregate#collation(collation, value)

Adds a collation

##### 参数：

  * `collation` &lt;[Object][]&gt; options

  * `value` &lt;[Boolean][]&gt;

##### 参见：

  * [mongodb](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#aggregate)

##### 示例：

Model.aggregate(..).collation({ locale: 'en_US', strength: 1 }).exec();
<!--sec data-title="源码" data-id="Aggregate_collation" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.collation = function(collation) {
  if (!this.options) {
    this.options = {};
  }
  this.options.collation = collation;
  return this;
};
```
<!--endsec-->


## Aggregate#cursor(options, options.batchSize, [options.useMongooseAggCursor])


Sets the cursor option option for the aggregation query (ignored for < 2.6.0).
Note the different syntax below: .exec() returns a cursor object, and no callback
is necessary.

##### 参数：

  * `options` &lt;[Object][]&gt;

  * `options.batchSize` <Number> set the cursor batch size

  * `[options.useMongooseAggCursor]` &lt;[Boolean][]&gt; use experimental mongoose-specific aggregation cursor (for eachAsync() and other query cursor semantics)

##### 参见：

  * [mongodb](http://mongodb.github.io/node-mongodb-native/2.0/api/AggregationCursor.html)

##### 示例：

```js
var cursor = Model.aggregate(..).cursor({ batchSize: 1000 }).exec();
cursor.each(function(error, doc) {
  // use doc
});
```

<!--sec data-title="源码" data-id="Aggregate_cursor" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.cursor = function(options) {
  if (!this.options) {
    this.options = {};
  }
  this.options.cursor = options || {};
  return this;
};
```
<!--endsec-->


## Aggregate#exec([callback])

Executes the aggregate pipeline on the currently bound Model.

##### 参数：

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Promise>

##### 参见：

  * [Promise]()

##### 示例：

```js
aggregate.exec(callback);

// Because a promise is returned, the `callback` is optional.
var promise = aggregate.exec();
promise.then(..);
```

<!--sec data-title="源码" data-id="Aggregate_exec" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.exec = function(callback) {
  if (!this._model) {
    throw new Error('Aggregate not bound to any Model');
  }
  var _this = this;
  var model = this._model;
  var Promise = PromiseProvider.get();
  var options = utils.clone(this.options || {});
  var pipeline = this._pipeline;
  var collection = this._model.collection;

  if (options && options.cursor) {
    if (options.cursor.async) {
      delete options.cursor.async;
      return new Promise.ES6(function(resolve) {
        if (!collection.buffer) {
          process.nextTick(function() {
            var cursor = collection.aggregate(pipeline, options);
            decorateCursor(cursor);
            resolve(cursor);
            callback && callback(null, cursor);
          });
          return;
        }
        collection.emitter.once('queue', function() {
          var cursor = collection.aggregate(pipeline, options);
          decorateCursor(cursor);
          resolve(cursor);
          callback && callback(null, cursor);
        });
      });
    } else if (options.cursor.useMongooseAggCursor) {
      delete options.cursor.useMongooseAggCursor;
      return new AggregationCursor(this);
    }
    var cursor = collection.aggregate(pipeline, options);
    decorateCursor(cursor);
    return cursor;
  }

  return new Promise.ES6(function(resolve, reject) {
    if (!pipeline.length) {
      var err = new Error('Aggregate has empty pipeline');
      if (callback) {
        callback(err);
      }
      reject(err);
      return;
    }

    prepareDiscriminatorPipeline(_this);

    model.hooks.execPre('aggregate', _this, function(error) {
      if (error) {
        var _opts = { error: error };
        return model.hooks.execPost('aggregate', _this, [null], _opts, function(error) {
          if (callback) {
            callback(error);
          }
          reject(error);
        });
      }

      collection.aggregate(pipeline, options, function(error, result) {
        var _opts = { error: error };
        model.hooks.execPost('aggregate', _this, [result], _opts, function(error, result) {
          if (error) {
            if (callback) {
              callback(error);
            }
            reject(error);
            return;
          }

          if (callback) {
            callback(null, result);
          }
          resolve(result);
        });
      });
    });
  });
};

```
<!--endsec-->

## Aggregate#explain(callback)

Execute the aggregation with explain

##### 参数：

  * `callback` &lt;[Function][]&gt;

##### 返回值：

  * <Promise>

##### 示例：

```js
Model.aggregate(..).explain(callback)
```

<!--sec data-title="源码" data-id="Aggregate_explain" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.explain = function(callback) {
  var _this = this;
  var Promise = PromiseProvider.get();
  return new Promise.ES6(function(resolve, reject) {
    if (!_this._pipeline.length) {
      var err = new Error('Aggregate has empty pipeline');
      if (callback) {
        callback(err);
      }
      reject(err);
      return;
    }

    prepareDiscriminatorPipeline(_this);

    _this._model
        .collection
        .aggregate(_this._pipeline, _this.options || {})
        .explain(function(error, result) {
          if (error) {
            if (callback) {
              callback(error);
            }
            reject(error);
            return;
          }

          if (callback) {
            callback(null, result);
          }
          resolve(result);
        });
  });
};
```
<!--endsec-->

## Aggregate#facet(facet)

Combines multiple aggregation pipelines.

##### 参数：

  * `facet` &lt;[Object][]&gt; options

##### 返回值：

  * <Aggregate> this

##### 参见：

  * [$facet](https://docs.mongodb.com/v3.4/reference/operator/aggregation/facet/)

##### 示例：

```js
Model.aggregate(...)
 .facet({
   books: [{ groupBy: '$author' }],
   price: [{ $bucketAuto: { groupBy: '$price', buckets: 2 } }]
 })
 .exec();
```

// Output: { books: [...], price: [{...}, {...}] }
<!--sec data-title="源码" data-id="Aggregate_facet" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.facet = function(options) {
  return this.append({$facet: options});
};
```
<!--endsec-->


## Aggregate#graphLookup(options)

Appends new custom $graphLookup operator(s) to this aggregate pipeline, performing a recursive search on a collection.

##### 参数：

  * `options` &lt;[Object][]&gt; to $graphLookup as described in the above link

##### 返回值：

  * <Aggregate>

##### 参见：

  * [$graphLookup](https://docs.mongodb.com/manual/reference/operator/aggregation/graphLookup/#pipe._S_graphLookup)

##### 注意：

 that graphLookup can only consume at most 100MB of memory, and does not allow disk use even if { allowDiskUse: true } is specified.

##### 示例：
```js
// Suppose we have a collection of courses, where a document might look like `{ _id: 0, name: 'Calculus', prerequisite: 'Trigonometry'}` and `{ _id: 0, name: 'Trigonometry', prerequisite: 'Algebra' }`
 aggregate.graphLookup({ from: 'courses', startWith: '$prerequisite', connectFromField: 'prerequisite', connectToField: 'name', as: 'prerequisites', maxDepth: 3 }) // this will recursively search the 'courses' collection up to 3 prerequisites
 ```


<!--sec data-title="源码" data-id="Aggregate_graphLooku" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.graphLookup = function(options) {
  var cloneOptions = {};
  if (options) {
    if (!utils.isObject(options)) {
      throw new TypeError('Invalid graphLookup() argument. Must be an object.');
    }

    utils.mergeClone(cloneOptions, options);
    var startWith = cloneOptions.startWith;

    if (startWith && typeof startWith === 'string') {
      cloneOptions.startWith = cloneOptions.startWith.charAt(0) === '$' ?
        cloneOptions.startWith :
        '$' + cloneOptions.startWith;
    }

  }
  return this.append({ $graphLookup: cloneOptions });
};

```
<!--endsec-->


## Aggregate#group(arg)

Appends a new custom $group operator to this aggregate pipeline.

##### 参数：

  * `arg` &lt;[Object][]&gt; $group operator contents

##### 返回值：

  * <Aggregate>

##### 参见：

  * [$group](http://docs.mongodb.org/manual/reference/aggregation/group/)

##### 示例：

```js
aggregate.group({ _id: "$department" });
```


## Aggregate#limit(num)

Appends a new $limit operator to this aggregate pipeline.

##### 参数：

  * `num` <Number> maximum number of records to pass to the next stage

##### 返回值：

  * <Aggregate>

##### 参见：

  * [$limit](http://docs.mongodb.org/manual/reference/aggregation/limit/)

##### 示例：

```js
aggregate.limit(10);
```


## Aggregate#lookup(options)

Appends new custom $lookup operator(s) to this aggregate pipeline.

##### 参数：

  * `options` &lt;[Object][]&gt; to $lookup as described in the above link

##### 返回值：

  * <Aggregate>

##### 参见：

  * [$lookup](https://docs.mongodb.org/manual/reference/operator/aggregation/lookup/#pipe._S_lookup)

##### 示例：

```js
aggregate.lookup({ from: 'users', localField: 'userId', foreignField: '_id', as: 'users' });
```

<!--sec data-title="源码" data-id="Aggregate_lookup" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.lookup = function(options) {
  return this.append({$lookup: options});
};
```
<!--endsec-->


## Aggregate#match(arg)

Appends a new custom $match operator to this aggregate pipeline.

##### 参数：

  * `arg` &lt;[Object][]&gt; $match operator contents

##### 返回值：

  * <Aggregate>

##### 参见：

  * [$match](http://docs.mongodb.org/manual/reference/aggregation/match/)

##### 示例：

```js
aggregate.match({ department: { $in: [ "sales", "engineering" ] } });
```



## Aggregate#model(model)

Binds this aggregate to a model.

##### 参数：

  * `model` <Model> the model to which the aggregate is to be bound

##### 返回值：

  * <Aggregate>

<!--sec data-title="源码" data-id="Aggregate_model" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.model = function(model) {
  this._model = model;
  if (model.schema != null) {
    if (this.options.readPreference == null &&
        model.schema.options.read != null) {
      this.options.readPreference = model.schema.options.read;
    }
    if (this.options.collation == null &&
        model.schema.options.collation != null) {
      this.options.collation = model.schema.options.collation;
    }
  }
  return this;
};
```
<!--endsec-->


## Aggregate#near(parameters)

Appends a new $geoNear operator to this aggregate pipeline.

##### 参数：

  * `parameters` &lt;[Object][]&gt;

##### 返回值：

  * <Aggregate>

##### 参见：

  * [$geoNear](http://docs.mongodb.org/manual/reference/aggregation/geoNear/)

##### 注意：

**MUST** be used as the first operator in the pipeline.

##### 示例：

```js
aggregate.near({
  near: [40.724, -73.997],
  distanceField: "dist.calculated", // required
  maxDistance: 0.008,
  query: { type: "public" },
  includeLocs: "dist.location",
  uniqueDocs: true,
  num: 5
});
```


## Aggregate#option(value)

Lets you set arbitrary options, for middleware or plugins.

##### 参数：

  * `value` &lt;[Object][]&gt; keys to merge into current options

##### 返回值：

  * <Aggregate> this

##### 参见：

  * [mongodb](http://docs.mongodb.org/manual/reference/command/aggregate/)

##### 示例：

```js
var agg = Model.aggregate(..).option({ allowDiskUse: true }); // Set the `allowDiskUse` option
agg.options; // `{ allowDiskUse: true }`
```

<!--sec data-title="源码" data-id="Aggregate_option" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.option = function(value) {
  for (var key in Object.keys(value)) {
    this.options[key] = value[key];
  }
  return this;
};
```
<!--endsec-->


## Aggregate#pipeline()

Returns the current pipeline

##### 返回值：

  * &lt;[Array][]&gt;

##### 示例：

```js
MyModel.aggregate().match({ test: 1 }).pipeline(); // [{ $match: { test: 1 } }]
```

<!--sec data-title="源码" data-id="Aggregate_pipeline" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.pipeline = function() {
  return this._pipeline;
};
```
<!--endsec-->


## Aggregate#project(arg)

Appends a new $project operator to this aggregate pipeline.

##### 参数：

  * `arg` <Object, String> field specification

##### 返回值：

  * <Aggregate>

##### 参见：

  * [projection](http://docs.mongodb.org/manual/reference/aggregation/project/)

Mongoose query selection syntax is also supported.

##### 示例：

```js
// include a, include b, exclude _id
aggregate.project("a b -_id");

// or you may use object notation, useful when
// you have keys already prefixed with a "-"
aggregate.project({a: 1, b: 1, _id: 0});

// reshaping documents
aggregate.project({
    newField: '$b.nested'
  , plusTen: { $add: ['$val', 10]}
  , sub: {
       name: '$a'
    }
})

// etc
aggregate.project({ salary_k: { $divide: [ "$salary", 1000 ] } });
```


<!--sec data-title="源码" data-id="Aggregate_project" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.project = function(arg) {
  var fields = {};

  if (typeof arg === 'object' && !util.isArray(arg)) {
    Object.keys(arg).forEach(function(field) {
      fields[field] = arg[field];
    });
  } else if (arguments.length === 1 && typeof arg === 'string') {
    arg.split(/\s+/).forEach(function(field) {
      if (!field) {
        return;
      }
      var include = field[0] === '-' ? 0 : 1;
      if (include === 0) {
        field = field.substring(1);
      }
      fields[field] = include;
    });
  } else {
    throw new Error('Invalid project() argument. Must be string or object');
  }

  return this.append({$project: fields});
};

```
<!--endsec-->


## Aggregate#read(pref, [tags])

Sets the readPreference option for the aggregation query.

##### 参数：

  * `pref` &lt;[String][]&gt; one of the listed preference options or their aliases

  * `[tags]` &lt;[Array][]&gt; optional tags for this query

##### 参见：

  * [mongodb](http://docs.mongodb.org/manual/applications/replication/#read-preference)

  * [driver](http://mongodb.github.com/node-mongodb-native/driver-articles/anintroductionto1_1and2_2.html#read-preferences)

##### 示例：

```js
Model.aggregate(..).read('primaryPreferred').exec(callback)
```

<!--sec data-title="源码" data-id="Aggregate_read" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.read = function(pref, tags) {
  if (!this.options) {
    this.options = {};
  }
  read.call(this, pref, tags);
  return this;
};
```
<!--endsec-->


## Aggregate#sample(size)

Appepnds new custom $sample operator(s) to this aggregate pipeline.

##### 参数：

  * `size` <Number> number of random documents to pick

##### 返回值：

  * <Aggregate>

##### 参见：

  * [$sample](https://docs.mongodb.org/manual/reference/operator/aggregation/sample/#pipe._S_sample)

##### 示例：

```js
aggregate.sample(3); // Add a pipeline that picks 3 random documents
```

<!--sec data-title="源码" data-id="Aggregate_sample" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.sample = function(size) {
  return this.append({$sample: {size: size}});
};
```
<!--endsec-->


## Aggregate#skip(num)

Appends a new $skip operator to this aggregate pipeline.

##### 参数：

  * `num` <Number> number of records to skip before next stage

##### 返回值：

  * <Aggregate>

##### 参见：

  * [$skip](http://docs.mongodb.org/manual/reference/aggregation/skip/)

##### 示例：

```js
aggregate.skip(10);

```


## Aggregate#sort(arg)

Appends a new $sort operator to this aggregate pipeline.

##### 参数：

  * `arg` <Object, String>

##### 返回值：

  * <Aggregate> this

##### 参见：

  * [$sort](http://docs.mongodb.org/manual/reference/aggregation/sort/)

If an object is passed, values allowed are asc, desc, ascending, descending, 1, and -1.

If a string is passed, it must be a space delimited list of path names. The sort order of each path is ascending unless the path name is prefixed with - which will be treated as descending.

##### 示例：

```js
// these are equivalent
aggregate.sort({ field: 'asc', test: -1 });
aggregate.sort('field -test');
```

<!--sec data-title="源码" data-id="Aggregate_sort" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.sort = function(arg) {
  // TODO refactor to reuse the query builder logic

  var sort = {};

  if (arg.constructor.name === 'Object') {
    var desc = ['desc', 'descending', -1];
    Object.keys(arg).forEach(function(field) {
      // If sorting by text score, skip coercing into 1/-1
      if (arg[field] instanceof Object && arg[field].$meta) {
        sort[field] = arg[field];
        return;
      }
      sort[field] = desc.indexOf(arg[field]) === -1 ? 1 : -1;
    });
  } else if (arguments.length === 1 && typeof arg === 'string') {
    arg.split(/\s+/).forEach(function(field) {
      if (!field) {
        return;
      }
      var ascend = field[0] === '-' ? -1 : 1;
      if (ascend === -1) {
        field = field.substring(1);
      }
      sort[field] = ascend;
    });
  } else {
    throw new TypeError('Invalid sort() argument. Must be a string or object.');
  }

  return this.append({$sort: sort});
};

```
<!--endsec-->


## Aggregate#then([resolve], [reject])

Provides promise for aggregate.

##### 参数：

  * `[resolve]` &lt;[Function][]&gt; successCallback

  * `[reject]` &lt;[Function][]&gt; errorCallback

##### 返回值：

  * <Promise>

##### 参见：

  * [Promise]()

##### 示例：

```js
Model.aggregate(..).then(successCallback, errorCallback);
```


<!--sec data-title="源码" data-id="Aggregate_then" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.then = function(resolve, reject) {
  return this.exec().then(resolve, reject);
};
```
<!--endsec-->


## Aggregate#unwind(fields)

Appends new custom $unwind operator(s) to this aggregate pipeline.

##### 参数：

  * `fields` &lt;[String][]&gt; the field(s) to unwind

##### 返回值：

  * <Aggregate>

##### 参见：

  * [$unwind](http://docs.mongodb.org/manual/reference/aggregation/unwind/)

##### 注意：

that the $unwind operator requires the path name to start with '$'.
Mongoose will prepend '$' if the specified field doesn't start '$'.

##### 示例：

```js
aggregate.unwind("tags");
aggregate.unwind("a", "b", "c");
```

<!--sec data-title="源码" data-id="Aggregate_unwind" data-show=true data-collapse=true ces-->
```js
Aggregate.prototype.unwind = function() {
  var args = utils.args(arguments);

  var res = [];
  for (var i = 0; i < args.length; ++i) {
    var arg = args[i];
    if (arg && typeof arg === 'object') {
      res.push({ $unwind: arg });
    } else if (typeof arg === 'string') {
      res.push({
        $unwind: (arg && arg.charAt(0) === '$') ? arg : '$' + arg
      });
    } else {
      throw new Error('Invalid arg "' + arg + '" to unwind(), ' +
        'must be string or object');
    }
  }

  return this.append.apply(this, res);
};
```
<!--endsec-->

----


# querystream.js

> 源码：[querystream.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/querystream.js)


## QueryStream#destroy([err])

Destroys the stream, closing the underlying cursor, which emits the close event. No more events will be emitted after the close event.

##### 参数：

  * `[err]` &lt;[Error][]&gt;

<!--sec data-title="源码" data-id="QueryStream_destroy" data-show=true data-collapse=true ces-->
```js
QueryStream.prototype.destroy = function(err) {
  if (this._destroyed) {
    return;
  }
  this._destroyed = true;
  this._running = false;
  this.readable = false;

  if (this._cursor) {
    this._cursor.close();
  }

  if (err) {
    this.emit('error', err);
  }

  this.emit('close');
};
```
<!--endsec-->


## QueryStream#pause()

Pauses this stream.

<!--sec data-title="源码" data-id="QueryStream_pause" data-show=true data-collapse=true ces-->
```js
QueryStream.prototype.pause = function() {
  this.paused = true;
};
```
<!--endsec-->


## QueryStream#pipe()

Pipes this query stream into another stream. This method is inherited from NodeJS Streams.

##### 参见：

  * [NodeJS](http://nodejs.org/api/stream.html)

##### 示例：

```js
query.stream().pipe(writeStream [, options])

```


## QueryStream(query, [options])

Provides a Node.js 0.8 style ReadStream interface for Queries.

##### 参数：

  * `query` <Query>

  * `[options]` &lt;[Object][]&gt;

##### 继承：

  * [NodeJS Stream](http://nodejs.org/docs/v0.8.21/api/stream.html#stream_readable_stream)

##### 事件：

  * `data`: emits a single Mongoose document

  * `error`: emits when an error occurs during streaming. This will emit before the close event.

  * `close`: emits when the stream reaches the end of the cursor or an error occurs, or the stream is manually destroyed. After this event, no more events are emitted.

```js
var stream = Model.find().stream();

stream.on('data', function (doc) {
  // do something with the mongoose document
}).on('error', function (err) {
  // handle the error
}).on('close', function () {
  // the stream is closed
});
```

The stream interface allows us to simply "plug-in" to other Node.js 0.8 style write streams.

```js
Model.where('created').gte(twoWeeksAgo).stream().pipe(writeStream);
```

##### 可用选项：

  * `transform`: optional function which accepts a mongoose document. The return value of the function will be emitted on data.

##### 示例：

```js
// JSON.stringify all documents before emitting
var stream = Thing.find().stream({ transform: JSON.stringify });
stream.pipe(writeStream);
```

##### 注意：

plugging into an HTTP response will *not* work out of the box. Those streams expect only strings or buffers to be emitted, so first formatting our documents as strings/buffers is necessary.

##### 注意：

these streams are Node.js 0.8 style read streams which differ from Node.js 0.10 style. Node.js 0.10 streams are not well tested yet and are not guaranteed to work.

<!--sec data-title="源码" data-id="QueryStream" data-show=true data-collapse=true ces-->
```js
function QueryStream(query, options) {
  Stream.call(this);

  this.query = query;
  this.readable = true;
  this.paused = false;
  this._cursor = null;
  this._destroyed = null;
  this._fields = null;
  this._buffer = null;
  this._inline = T_INIT;
  this._running = false;
  this._transform = options && typeof options.transform === 'function'
      ? options.transform
      : K;

  // give time to hook up events
  var _this = this;
  process.nextTick(function() {
    _this._init();
  });
}
```
<!--endsec-->


## QueryStream#resume()

Resumes this stream.

<!--sec data-title="源码" data-id="QueryStream_resume" data-show=true data-collapse=true ces-->
```js
QueryStream.prototype.resume = function() {
  this.paused = false;

  if (!this._cursor) {
    // cannot start if not initialized
    return;
  }

  // are we within the trampoline?
  if (T_INIT === this._inline) {
    return;
  }

  if (!this._running) {
    // outside QueryStream control, need manual restart
    return this._next();
  }
};
```
<!--endsec-->



## QueryStream#paused

Flag stating whether or not this stream is paused.

<!--sec data-title="源码" data-id="QueryStream_paused" data-show=true data-collapse=true ces-->
```js
QueryStream.prototype.paused;

// trampoline flags
var T_INIT = 0;
var T_IDLE = 1;
var T_CONT = 2;
```
<!--endsec-->


## QueryStream#readable

Flag stating whether or not this stream is readable.

<!--sec data-title="源码" data-id="QueryStream_readable" data-show=true data-collapse=true ces-->
```js
QueryStream.prototype.readable;
```
<!--endsec-->

----


# services/cursor/eachAsync.js

> 源码：[services/cursor/eachAsync.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/services/cursor/eachAsync.js)


## module.exports(next, fn, options, [callback])

Execute fn for every document in the cursor. If fn returns a promise,
will wait for the promise to resolve before iterating on to the next one.
Returns a promise that resolves when done.

##### 参数：

  * `next` &lt;[Function][]&gt; the thunk to call to get the next document

  * `fn` &lt;[Function][]&gt;

  * `options` &lt;[Object][]&gt;

  * `[callback]` &lt;[Function][]&gt; executed when all docs have been processed

##### 返回值：

  * <Promise>


----

# error/index.js

> 源码：[error/index.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/error/index.js)

## MongooseError(msg)

MongooseError constructor


##### 参数：

  * `msg` &lt;[String][]&gt; Error message


##### 继承：

  * [Error](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Error)

<!--sec data-title="源码" data-id="MongooseError" data-show=true data-collapse=true ces-->
```js
function MongooseError(msg) {
  Error.call(this);
  if (Error.captureStackTrace) {
    Error.captureStackTrace(this);
  } else {
    this.stack = new Error().stack;
  }
  this.message = msg;
  this.name = 'MongooseError';
}
```
<!--endsec-->


## MongooseError.DocumentNotFoundError


This error will be called when save() fails because the underlying
document was not found. The constructor takes one parameter, the
conditions that mongoose passed to update() when trying to update
the document.

<!--sec data-title="源码" data-id="MongooseError_DocumentNotFoundError" data-show=true data-collapse=true ces-->
```js
MongooseError.DocumentNotFoundError = require('./notFound');
```
<!--endsec-->


## MongooseError.messages
The default built-in validator error messages.

<!--sec data-title="源码" data-id="MongooseError_messages" data-show=true data-collapse=true ces-->
```js
MongooseError.messages = require('./messages');

// backward compat
MongooseError.Messages = MongooseError.messages;
```
<!--endsec-->

##### 参见：

  * [Error.messages]()



-----


# error/messages.js

> 源码：[error/messages.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/error/messages.js)


## MongooseError.messages()

The default built-in validator error messages. These may be customized.

<!--sec data-title="源码" data-id="MongooseError_messages_" data-show=true data-collapse=true ces-->
```js
var msg = module.exports = exports = {};

msg.DocumentNotFoundError = null;

msg.general = {};
msg.general.default = 'Validator failed for path `{PATH}` with value `{VALUE}`';
msg.general.required = 'Path `{PATH}` is required.';

msg.Number = {};
msg.Number.min = 'Path `{PATH}` ({VALUE}) is less than minimum allowed value ({MIN}).';
msg.Number.max = 'Path `{PATH}` ({VALUE}) is more than maximum allowed value ({MAX}).';

msg.Date = {};
msg.Date.min = 'Path `{PATH}` ({VALUE}) is before minimum allowed value ({MIN}).';
msg.Date.max = 'Path `{PATH}` ({VALUE}) is after maximum allowed value ({MAX}).';

msg.String = {};
msg.String.enum = '`{VALUE}` is not a valid enum value for path `{PATH}`.';
msg.String.match = 'Path `{PATH}` is invalid ({VALUE}).';
msg.String.minlength = 'Path `{PATH}` (`{VALUE}`) is shorter than the minimum allowed length ({MINLENGTH}).';
msg.String.maxlength = 'Path `{PATH}` (`{VALUE}`) is longer than the maximum allowed length ({MAXLENGTH}).';
```
<!--endsec-->

```js
// customize within each schema or globally like so
var mongoose = require('mongoose');
mongoose.Error.messages.String.enum  = "Your custom message for {PATH}.";
```

As you might have noticed, error messages support basic templating

  * `{PATH}` is replaced with the invalid document path
  * `{VALUE}` is replaced with the invalid value
  * `{TYPE}` is replaced with the validator type such as "regexp", "min", or "user defined"
  * `{MIN}` is replaced with the declared min value for the Number.min validator
  * `{MAX}` is replaced with the declared max value for the Number.max validator

Click the "show code" link below to see all defaults.



-----


# error/validation.js

> 源码：[error/validation.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/error/validation.js)


## ValidationError#toString()

Console.log helper

<!--sec data-title="源码" data-id="ValidationError_toString" data-show=true data-collapse=true ces-->
```js
ValidationError.prototype.toString = function() {
  return this.name + ': ' + _generateMessage(this);
};
```
<!--endsec-->

-----

# model.js

> 源码：[model.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/model.js)


## Model#$where(argument)

Creates a Query and specifies a $where condition.

##### 参数：

  * `argument` &lt;[String][], [Function][]&gt;is a javascript string or anonymous function

##### 返回值：

  * <Query>

##### 参见：

  * [Query.$where](http://mongoosejs.com/docs/api.html#query_Query-%24where)

Sometimes you need to query for things in mongodb using a JavaScript expression. You can do so via find({ $where: javascript }), or you can use the mongoose shortcut method $where via a Query chain or from your mongoose Model.

```js
Blog.$where('this.username.indexOf("val") !== -1').exec(function (err, docs) {});
```

## Model#increment()

Signal that we desire an increment of this documents version.

##### 参见：

  * [versionKeys]()

##### 示例：

```js
Model.findById(id, function (err, doc) {
  doc.increment();
  doc.save(function (err) { .. })
})
```

<!--sec data-title="源码" data-id="Model_increment" data-show=true data-collapse=true ces-->
```js
Model.prototype.increment = function increment() {
  this.$__.version = VERSION_ALL;
  return this;
};
```
<!--endsec-->


## Model#model(name)

Returns another Model instance.

##### 参数：

  * name &lt;[String][]&gt; model name

##### 示例：

```js
var doc = new Tank;
doc.model('User').findById(id, callback);
```

<!--sec data-title="源码" data-id="Model_model" data-show=true data-collapse=true ces-->
```js
Model.prototype.model = function model(name) {
  return this.db.model(name);
};
```
<!--endsec-->

## Model(doc)

Model constructor

##### 参数：

  * `doc` &lt;[Object][]&gt; values with which to create the document

##### 继承：

  * [Document]()

##### 事件：

  * `error`: If listening to this event, 'error' is emitted when a document was saved without passing a callback and an error occurred. If not listening, the event bubbles to the connection used to create this Model.

  * `index`: Emitted after Model#ensureIndexes completes. If an error occurred it is passed with the event.

  * `index-single-start`: Emitted when an individual index starts within Model#ensureIndexes. The fields and options being used to build the index are also passed with the event.

  * `index-single-done`: Emitted when an individual index finishes within Model#ensureIndexes. If an error occurred it is passed with the event. The fields, options, and index name are also passed.

Provides the interface to MongoDB collections as well as creates document instances.

<!--sec data-title="源码" data-id="Model" data-show=true data-collapse=true ces-->
```js
function Model(doc, fields, skipId) {
  if (fields instanceof Schema) {
    throw new TypeError('2nd argument to `Model` must be a POJO or string, ' +
      '**not** a schema. Make sure you\'re calling `mongoose.model()`, not ' +
      '`mongoose.Model()`.');
  }
  Document.call(this, doc, fields, skipId, true);
}
```
<!--endsec-->


## Model#remove([fn])

Removes this document from the db.

##### 参数：

  * `[fn]` <function(err, product)> optional callback

##### 返回值：

  * <Promise> Promise

##### 示例：

```js
product.remove(function (err, product) {
  if (err) return handleError(err);
  Product.findById(product._id, function (err, product) {
    console.log(product) // null
  })
})
```

As an extra measure of flow control, remove will return a Promise (bound to fn if passed) so it could be chained, or hooked to recive errors

##### 示例：

```js
product.remove().then(function (product) {
   ...
}).catch(function (err) {
   assert.ok(err)
})
```

<!--sec data-title="源码" data-id="Model_remove" data-show=true data-collapse=true ces-->
```js
Model.prototype.remove = function remove(options, fn) {
  if (typeof options === 'function') {
    fn = options;
    options = undefined;
  }

  var _this = this;

  if (!options) {
    options = {};
  }

  if (this.$__.removing) {
    if (fn) {
      this.$__.removing.then(
          function(res) { fn(null, res); },
          function(err) { fn(err); });
    }
    return this;
  }
  if (this.$__.isDeleted) {
    setImmediate(function() {
      fn(null, _this);
    });
    return this;
  }

  var Promise = PromiseProvider.get();

  if (fn) {
    fn = this.constructor.$wrapCallback(fn);
  }

  this.$__.removing = new Promise.ES6(function(resolve, reject) {
    var where = _this.$__where();
    if (where instanceof Error) {
      reject(where);
      fn && fn(where);
      return;
    }

    if (!options.safe && _this.schema.options.safe) {
      options.safe = _this.schema.options.safe;
    }

    _this.collection.remove(where, options, function(err) {
      if (!err) {
        _this.$__.isDeleted = true;
        _this.emit('remove', _this);
        _this.constructor.emit('remove', _this);
        resolve(_this);
        fn && fn(null, _this);
        return;
      }
      _this.$__.isDeleted = false;
      reject(err);
      fn && fn(err);
    });
  });
  return this.$__.removing;
};
```
<!--endsec-->


## Model#save([options], [options.safe], [options.validateBeforeSave], [fn])

Saves this document.

##### 参数：

  * `[options]` &lt;[Object][]&gt; options optional options

  * `[options.safe]` &lt;[Object][]&gt; overrides schema's safe option

  * `[options.validateBeforeSave]` &lt;[Boolean][]&gt; set to false to save without validating.

  * `[fn]` &lt;[Function][]&gt; optional callback

##### 返回值：

  * <Promise> Promise

##### 参见：

  * [middleware](/Library/mongoose/docs/middleware.md)

##### 示例：

```js
product.sold = Date.now();
product.save(function (err, product, numAffected) {
  if (err) ..
})
```

The callback will receive three parameters

  * `err` if an error occurred
  * `product` which is the saved product
  * `numAffected` will be 1 when the document was successfully persisted to MongoDB, otherwise 0. Unless you tweak mongoose's internals, you don't need to worry about checking this parameter for errors - checking err is sufficient to make sure your document was properly saved.


As an extra measure of flow control, save will return a Promise.

##### 示例：

```js
product.save().then(function(product) {
   ...
});
```

For legacy reasons, mongoose stores object keys in reverse order on initial
save. That is, { a: 1, b: 2 } will be saved as { b: 2, a: 1 } in
MongoDB. To override this behavior, set
[the toObject.retainKeyOrder option](http://mongoosejs.com/docs/api.html#document_Document-toObject)
to true on your schema.

<!--sec data-title="源码" data-id="Model_save" data-show=true data-collapse=true ces-->
```js
Model.prototype.save = function(options, fn) {
  if (typeof options === 'function') {
    fn = options;
    options = undefined;
  }

  if (!options) {
    options = {};
  }

  if (fn) {
    fn = this.constructor.$wrapCallback(fn);
  }

  return this.$__save(options, fn);
};
```
<!--endsec-->

## Model.aggregate([...], [callback])

Performs [aggregations]() on the models collection.

<!--sec data-title="源码" data-id="Model_aggregate" data-show=true data-collapse=true ces-->
```js
Model.aggregate = function aggregate() {
  var args = [].slice.call(arguments),
      aggregate,
      callback;

  if (typeof args[args.length - 1] === 'function') {
    callback = args.pop();
  }

  if (args.length === 1 && util.isArray(args[0])) {
    aggregate = new Aggregate(args[0]);
  } else {
    aggregate = new Aggregate(args);
  }

  aggregate.model(this);

  if (typeof callback === 'undefined') {
    return aggregate;
  }

  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  aggregate.exec(callback);
};
```
<!--endsec-->

##### 参数：

  * `[...]` <Object, Array> aggregation pipeline operator(s) or operator array

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Aggregate, Promise>

##### 参见：

  * [Aggregate](http://mongoosejs.com/docs/api.html#aggregate_Aggregate)

  * [MongoDB](http://docs.mongodb.org/manual/applications/aggregation/)

If a callback is passed, the aggregate is executed and a Promise is returned. If a callback is not passed, the aggregate itself is returned.

This function does not trigger any middleware.

##### 示例：

```js
// Find the max balance of all accounts
Users.aggregate(
  { $group: { _id: null, maxBalance: { $max: '$balance' }}},
  { $project: { _id: 0, maxBalance: 1 }},
  function (err, res) {
    if (err) return handleError(err);
    console.log(res); // [ { maxBalance: 98000 } ]
  });

// Or use the aggregation pipeline builder.
Users.aggregate()
  .group({ _id: null, maxBalance: { $max: '$balance' } })
  .select('-id maxBalance')
  .exec(function (err, res) {
    if (err) return handleError(err);
    console.log(res); // [ { maxBalance: 98 } ]
});
```

##### 注意：

  * Arguments are not cast to the model's schema because $project operators allow redefining the "shape" of the documents at any stage of the pipeline, which may leave documents in an incompatible format.
  * The documents returned are plain javascript objects, not mongoose documents (since any shape of document can be returned).
  * Requires MongoDB >= 2.1


## Model.bulkWrite(ops, [options], [callback])

Sends multiple insertOne, updateOne, updateMany, replaceOne,
deleteOne, and/or deleteMany operations to the MongoDB server in one
command. This is faster than sending multiple independent operations (like)
if you use create()) because with bulkWrite() there is only one round
trip to MongoDB.

<!--sec data-title="源码" data-id="Model_bulkWrite" data-show=true data-collapse=true ces-->
```js
Model.bulkWrite = function(ops, options, callback) {
  var Promise = PromiseProvider.get();
  var _this = this;
  if (typeof options === 'function') {
    callback = options;
    options = null;
  }
  if (callback) {
    callback = this.$wrapCallback(callback);
  }
  options = options || {};

  var validations = ops.map(function(op) {
    if (op['insertOne']) {
      return function(callback) {
        op['insertOne']['document'] = new _this(op['insertOne']['document']);
        op['insertOne']['document'].validate({ __noPromise: true }, function(error) {
          if (error) {
            return callback(error);
          }
          callback(null);
        });
      };
    } else if (op['updateOne']) {
      op = op['updateOne'];
      return function(callback) {
        try {
          op['filter'] = cast(_this.schema, op['filter']);
          op['update'] = castUpdate(_this.schema, op['update'],
            _this.schema.options.strict);
          if (op.setDefaultsOnInsert) {
            setDefaultsOnInsert(op['filter'], _this.schema, op['update'], {
              setDefaultsOnInsert: true,
              upsert: op.upsert
            });
          }
        } catch (error) {
          return callback(error);
        }

        callback(null);
      };
    } else if (op['updateMany']) {
      op = op['updateMany'];
      return function(callback) {
        try {
          op['filter'] = cast(_this.schema, op['filter']);
          op['update'] = castUpdate(_this.schema, op['update'], {
            strict: _this.schema.options.strict,
            overwrite: false
          });
          if (op.setDefaultsOnInsert) {
            setDefaultsOnInsert(op['filter'], _this.schema, op['update'], {
              setDefaultsOnInsert: true,
              upsert: op.upsert
            });
          }
        } catch (error) {
          return callback(error);
        }

        callback(null);
      };
    } else if (op['replaceOne']) {
      return function(callback) {
        try {
          op['replaceOne']['filter'] = cast(_this.schema,
            op['replaceOne']['filter']);
        } catch (error) {
          return callback(error);
        }

        // set `skipId`, otherwise we get "_id field cannot be changed"
        op['replaceOne']['replacement'] =
          new _this(op['replaceOne']['replacement'], null, true);
        op['replaceOne']['replacement'].validate({ __noPromise: true }, function(error) {
          if (error) {
            return callback(error);
          }
          callback(null);
        });
      };
    } else if (op['deleteOne']) {
      return function(callback) {
        try {
          op['deleteOne']['filter'] = cast(_this.schema,
            op['deleteOne']['filter']);
        } catch (error) {
          return callback(error);
        }

        callback(null);
      };
    } else if (op['deleteMany']) {
      return function(callback) {
        try {
          op['deleteMany']['filter'] = cast(_this.schema,
            op['deleteMany']['filter']);
        } catch (error) {
          return callback(error);
        }

        callback(null);
      };
    } else {
      return function(callback) {
        callback(new Error('Invalid op passed to `bulkWrite()`'));
      };
    }
  });

  var promise = new Promise.ES6(function(resolve, reject) {
    parallel(validations, function(error) {
      if (error) {
        callback && callback(error);
        return reject(error);
      }

      _this.collection.bulkWrite(ops, options, function(error, res) {
        if (error) {
          callback && callback(error);
          return reject(error);
        }

        callback && callback(null, res);
        resolve(res);
      });
    });
  });

  return promise;
};

```
<!--endsec-->
##### 参数：

  * `ops` &lt;[Array][]&gt;

  * `[options]` &lt;[Object][]&gt;

  * `[callback]` &lt;[Function][]&gt; callback <code>function(error, bulkWriteOpResult) {}</code>

##### 返回值：

  * <Promise> resolves to a `BulkWriteOpResult` if the operation succeeds

##### 参见：

  * [writeOpResult](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#~BulkWriteOpResult)

Mongoose will perform casting on all operations you provide.

This function does not trigger any middleware, not save() nor update().
If you need to trigger
save() middleware for every document use [create()]() instead.

##### 示例：

```js
Character.bulkWrite([
  {
    insertOne: {
      document: {
        name: 'Eddard Stark',
        title: 'Warden of the North'
      }
    }
  },
  {
    updateOne: {
      filter: { name: 'Eddard Stark' },
      // If you were using the MongoDB driver directly, you'd need to do
      // `update: { $set: { title: ... } }` but mongoose adds $set for
      // you.
      update: { title: 'Hand of the King' }
    }
  },
  {
    deleteOne: {
      {
        filter: { name: 'Eddard Stark' }
      }
    }
  }
]).then(handleResult);
```

## Model.count(conditions, [callback])

Counts number of matching documents in a database collection.

<!--sec data-title="源码" data-id="Model_coun" data-show=true data-collapse=true ces-->
```js
Model.count = function count(conditions, callback) {
  if (typeof conditions === 'function') {
    callback = conditions;
    conditions = {};
  }

  // get the mongodb collection object
  var mq = new this.Query({}, {}, this, this.collection);

  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  return mq.count(conditions, callback);
};
```
<!--endsec-->

##### 参数：

  * `conditions` &lt;[Object][]&gt;

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 示例：

```js
Adventure.count({ type: 'jungle' }, function (err, count) {
  if (err) ..
  console.log('there are %d jungle adventures', count);
});
```



## Model.create(doc(s), [callback])


Shortcut for saving one or more documents to the database.
MyModel.create(docs) does new MyModel(doc).save() for every doc in
docs.

<!--sec data-title="源码" data-id="Model_creat" data-show=true data-collapse=true ces-->
```js
Model.create = function create(doc, callback) {
  var args;
  var cb;
  var discriminatorKey = this.schema.options.discriminatorKey;

  if (Array.isArray(doc)) {
    args = doc;
    cb = callback;
  } else {
    var last = arguments[arguments.length - 1];
    // Handle falsy callbacks re: #5061
    if (typeof last === 'function' || !last) {
      cb = last;
      args = utils.args(arguments, 0, arguments.length - 1);
    } else {
      args = utils.args(arguments);
    }
  }

  var Promise = PromiseProvider.get();
  var _this = this;
  if (cb) {
    cb = this.$wrapCallback(cb);
  }

  var promise = new Promise.ES6(function(resolve, reject) {
    if (args.length === 0) {
      setImmediate(function() {
        cb && cb(null);
        resolve(null);
      });
      return;
    }

    var toExecute = [];
    var firstError;
    args.forEach(function(doc) {
      toExecute.push(function(callback) {
        var Model = _this.discriminators && doc[discriminatorKey] ?
          _this.discriminators[doc[discriminatorKey]] :
          _this;
        var toSave = doc;
        var callbackWrapper = function(error, doc) {
          if (error) {
            if (!firstError) {
              firstError = error;
            }
            return callback(null, { error: error });
          }
          callback(null, { doc: doc });
        };

        if (!(toSave instanceof Model)) {
          try {
            toSave = new Model(toSave);
          } catch (error) {
            return callbackWrapper(error);
          }
        }

        // Hack to avoid getting a promise because of
        // $__registerHooksFromSchema
        if (toSave.$__original_save) {
          toSave.$__original_save({ __noPromise: true }, callbackWrapper);
        } else {
          toSave.save({ __noPromise: true }, callbackWrapper);
        }
      });
    });

    parallel(toExecute, function(error, res) {
      var savedDocs = [];
      var len = res.length;
      for (var i = 0; i < len; ++i) {
        if (res[i].doc) {
          savedDocs.push(res[i].doc);
        }
      }

      if (firstError) {
        if (cb) {
          cb(firstError, savedDocs);
        } else {
          reject(firstError);
        }
        return;
      }

      if (doc instanceof Array) {
        resolve(savedDocs);
        cb && cb.call(_this, null, savedDocs);
      } else {
        resolve.apply(promise, savedDocs);
        if (cb) {
          cb.apply(_this, [null].concat(savedDocs));
        }
      }
    });
  });

  return promise;
};
```
<!--endsec-->
##### 参数：

  * `doc(s)` <Array, Object, *>

  * `[callback]` &lt;[Function][]&gt; callback

##### 返回值：

  * <Promise>

**This function triggers the following middleware**

  * save()

##### 示例：

```js
// pass individual docs
Candy.create({ type: 'jelly bean' }, { type: 'snickers' }, function (err, jellybean, snickers) {
  if (err) // ...
});

// pass an array
var array = [{ type: 'jelly bean' }, { type: 'snickers' }];
Candy.create(array, function (err, candies) {
  if (err) // ...

  var jellybean = candies[0];
  var snickers = candies[1];
  // ...
});

// callback is optional; use the returned promise if you like:
var promise = Candy.create({ type: 'jawbreaker' });
promise.then(function (jawbreaker) {
  // ...
})
```


## Model.createIndexes([options], [cb])


Similar to ensureIndexes(), except for it uses the createIndex
function. The ensureIndex() function checks to see if an index with that
name already exists, and, if not, does not attempt to create the index.
createIndex() bypasses this check.

<!--sec data-title="源码" data-id="Model_createIndexes" data-show=true data-collapse=true ces-->
```js
Model.createIndexes = function createIndexes(options, callback) {
  if (typeof options === 'function') {
    callback = options;
    options = {};
  }
  options = options || {};
  options.createIndex = true;
  return this.ensureIndexes(options, callback);
};

function _ensureIndexes(model, options, callback) {
  var indexes = model.schema.indexes();
  options = options || {};

  var done = function(err) {
    if (err && model.schema.options.emitIndexErrors) {
      model.emit('error', err);
    }
    model.emit('index', err);
    callback && callback(err);
  };

  if (!indexes.length) {
    setImmediate(function() {
      done();
    });
    return;
  }
  // Indexes are created one-by-one to support how MongoDB < 2.4 deals
  // with background indexes.

  var indexSingleDone = function(err, fields, options, name) {
    model.emit('index-single-done', err, fields, options, name);
  };
  var indexSingleStart = function(fields, options) {
    model.emit('index-single-start', fields, options);
  };

  var create = function() {
    if (options._automatic) {
      if (model.schema.options.autoIndex === false ||
          (model.schema.options.autoIndex == null && model.db.config.autoIndex === false)) {
        return done();
      }
    }

    var index = indexes.shift();
    if (!index) return done();

    var indexFields = index[0];
    var indexOptions = index[1];
    _handleSafe(options);

    indexSingleStart(indexFields, options);
    var methodName = options.createIndex ? 'createIndex' : 'ensureIndex';
    model.collection[methodName](indexFields, indexOptions, utils.tick(function(err, name) {
      indexSingleDone(err, indexFields, indexOptions, name);
      if (err) {
        return done(err);
      }
      create();
    }));
  };

  setImmediate(function() {
    // If buffering is off, do this manually.
    if (options._automatic && !model.collection.collection) {
      model.collection.addQueue(create, []);
    } else {
      create();
    }
  });
}

function _handleSafe(options) {
  if (options.safe) {
    if (typeof options.safe === 'boolean') {
      options.w = options.safe;
      delete options.safe;
    }
    if (typeof options.safe === 'object') {
      options.w = options.safe.w;
      options.j = options.safe.j;
      options.wtimeout = options.safe.wtimeout;
      delete options.safe;
    }
  }
}

```
<!--endsec-->
##### 参数：

  * `[options] `&lt;[Object][]&gt; internal options

  * `[cb]` &lt;[Function][]&gt; optional callback

##### 返回值：

  * <Promise>



## Model.deleteMany(conditions, [callback])


Deletes all of the documents that match conditions from the collection.
Behaves like remove(), but deletes all documents that match conditions
regardless of the single option.

<!--sec data-title="源码" data-id="Model_deleteMany" data-show=true data-collapse=true ces-->
```js
Model.deleteMany = function deleteMany(conditions, callback) {
  if (typeof conditions === 'function') {
    callback = conditions;
    conditions = {};
  }

  // get the mongodb collection object
  var mq = new this.Query(conditions, {}, this, this.collection);

  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  return mq.deleteMany(callback);
};
```
<!--endsec-->

##### 参数：

  * `conditions` &lt;[Object][]&gt;

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 示例：

```js
Character.deleteMany({ name: /Stark/, age: { $gte: 18 } }, function (err) {});
```

##### 注意：

Like `Model.remove()`, this function does not trigger pre('remove') or post('remove') hooks.



## Model.deleteOne(conditions, [callback])


Deletes the first document that matches conditions from the collection.
Behaves like remove(), but deletes at most one document regardless of the
single option.

<!--sec data-title="源码" data-id="Model_deleteOne" data-show=true data-collapse=true ces-->
```js
Model.deleteOne = function deleteOne(conditions, callback) {
  if (typeof conditions === 'function') {
    callback = conditions;
    conditions = {};
  }

  // get the mongodb collection object
  var mq = new this.Query(conditions, {}, this, this.collection);

  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  return mq.deleteOne(callback);
};
```
<!--endsec-->

##### 参数：

  * `conditions` &lt;[Object][]&gt;

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 示例：

```js
Character.deleteOne({ name: 'Eddard Stark' }, function (err) {});
```

##### 注意：

Like `Model.remove()`, this function does not trigger pre('remove') or post('remove') hooks.

## Model.discriminator(name, schema)

Adds a discriminator type.

<!--sec data-title="源码" data-id="Model_discriminator" data-show=true data-collapse=true ces-->
```js
Model.discriminator = function(name, schema) {
  var model;
  if (typeof name === 'function') {
    model = name;
    name = utils.getFunctionName(model);
    if (!(model.prototype instanceof Model)) {
      throw new Error('The provided class ' + name + ' must extend Model');
    }
  }

  schema = discriminator(this, name, schema);
  if (this.db.models[name]) {
    throw new OverwriteModelError(name);
  }

  schema.$isRootDiscriminator = true;

  model = this.db.model(model || name, schema, this.collection.name);
  this.discriminators[name] = model;
  var d = this.discriminators[name];
  d.prototype.__proto__ = this.prototype;
  Object.defineProperty(d, 'baseModelName', {
    value: this.modelName,
    configurable: true,
    writable: false
  });

  // apply methods and statics
  applyMethods(d, schema);
  applyStatics(d, schema);

  return d;
};

// Model (class) features
```
<!--endsec-->

##### 参数：

  * `name` &lt;[String][]&gt; discriminator model name

  * `schema` <Schema> discriminator model schema

##### 示例：

```js
function BaseSchema() {
  Schema.apply(this, arguments);

  this.add({
    name: String,
    createdAt: Date
  });
}
util.inherits(BaseSchema, Schema);

var PersonSchema = new BaseSchema();
var BossSchema = new BaseSchema({ department: String });

var Person = mongoose.model('Person', PersonSchema);
var Boss = Person.discriminator('Boss', BossSchema);
```


## Model.distinct(field, [conditions], [callback])

Creates a Query for a distinct operation.

<!--sec data-title="源码" data-id="Model_distinct" data-show=true data-collapse=true ces-->
```js
Model.distinct = function distinct(field, conditions, callback) {
  // get the mongodb collection object
  var mq = new this.Query({}, {}, this, this.collection);

  if (typeof conditions === 'function') {
    callback = conditions;
    conditions = {};
  }
  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  return mq.distinct(field, conditions, callback);
};
```
<!--endsec-->

##### 参数：

  * `field` &lt;[String][]&gt;

  * `[conditions]` &lt;[Object][]&gt; optional

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

Passing a callback immediately executes the query.

##### 示例：

```js
Link.distinct('url', { clicks: {$gt: 100}}, function (err, result) {
  if (err) return handleError(err);

  assert(Array.isArray(result));
  console.log('unique urls with more than 100 clicks', result);
})

var query = Link.distinct('url');
query.exec(callback);
```


## Model.ensureIndexes([options], [cb])

Sends createIndex commands to mongo for each index declared in the schema.
The createIndex commands are sent in series.

<!--sec data-title="源码" data-id="Model_ensureIndexes" data-show=true data-collapse=true ces-->
```js
Model.ensureIndexes = function ensureIndexes(options, callback) {
  if (typeof options === 'function') {
    callback = options;
    options = null;
  }

  if (options && options.__noPromise) {
    _ensureIndexes(this, options, callback);
    return;
  }

  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  var _this = this;
  var Promise = PromiseProvider.get();
  return new Promise.ES6(function(resolve, reject) {
    _ensureIndexes(_this, options || {}, function(error) {
      if (error) {
        callback && callback(error);
        reject(error);
      }
      callback && callback();
      resolve();
    });
  });
};
```
<!--endsec-->

##### 参数：

  * `[options]` &lt;[Object][]&gt; internal options

  * `[cb]` &lt;[Function][]&gt; optional callback

##### 返回值：

  * <Promise>

##### 示例：

```js
Event.ensureIndexes(function (err) {
  if (err) return handleError(err);
});
```

After completion, an index event is emitted on this Model passing an error if one occurred.

##### 示例：

```js
var eventSchema = new Schema({ thing: { type: 'string', unique: true }})
var Event = mongoose.model('Event', eventSchema);

Event.on('index', function (err) {
  if (err) console.error(err); // error occurred during index creation
})
```

##### 注意：

It is not recommended that you run this in production. Index creation may impact database performance depending on your load. Use with caution.



## Model.find(conditions, [projection], [options], [callback])

Finds documents

<!--sec data-title="源码" data-id="Model_find" data-show=true data-collapse=true ces-->
```js
Model.find = function find(conditions, projection, options, callback) {
  if (typeof conditions === 'function') {
    callback = conditions;
    conditions = {};
    projection = null;
    options = null;
  } else if (typeof projection === 'function') {
    callback = projection;
    projection = null;
    options = null;
  } else if (typeof options === 'function') {
    callback = options;
    options = null;
  }

  var mq = new this.Query({}, {}, this, this.collection);
  mq.select(projection);
  mq.setOptions(options);
  if (this.schema.discriminatorMapping &&
      this.schema.discriminatorMapping.isRoot &&
      mq.selectedInclusively()) {
    // Need to select discriminator key because original schema doesn't have it
    mq.select(this.schema.options.discriminatorKey);
  }

  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  return mq.find(conditions, callback);
};

```
<!--endsec-->

##### 参数：

  * `conditions` &lt;[Object][]&gt;

  * `[projection]` &lt;[Object][]&gt; optional fields to return (http://bit.ly/1HotzBo)

  * `[options]` &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 参见：

  * [field selection](http://mongoosejs.com/docs/api.html#query_Query-select)

  * [promise](http://mongoosejs.com/docs/api.html#promise-js)

The conditions are cast to their respective SchemaTypes before the command is sent.

##### 示例：

```js
// named john and at least 18
MyModel.find({ name: 'john', age: { $gte: 18 }});

// executes immediately, passing results to callback
MyModel.find({ name: 'john', age: { $gte: 18 }}, function (err, docs) {});

// name LIKE john and only selecting the "name" and "friends" fields, executing immediately
MyModel.find({ name: /john/i }, 'name friends', function (err, docs) { })

// passing options
MyModel.find({ name: /john/i }, null, { skip: 10 })

// passing options and executing immediately
MyModel.find({ name: /john/i }, null, { skip: 10 }, function (err, docs) {});

// executing a query explicitly
var query = MyModel.find({ name: /john/i }, null, { skip: 10 })
query.exec(function (err, docs) {});

// using the promise returned from executing a query
var query = MyModel.find({ name: /john/i }, null, { skip: 10 });
var promise = query.exec();
promise.addBack(function (err, docs) {});
```


## Model.findById(id, [projection], [options], [callback])


Finds a single document by its _id field. findById(id) is almost*
equivalent to findOne({ _id: id }). If you want to query by a document's
_id, use findById() instead of findOne().

<!--sec data-title="源码" data-id="Model_findById" data-show=true data-collapse=true ces-->
```js
Model.findById = function findById(id, projection, options, callback) {
  if (typeof id === 'undefined') {
    id = null;
  }

  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  return this.findOne({_id: id}, projection, options, callback);
};
```
<!--endsec-->

##### 参数：

  * `id` <Object, String, Number> value of <code>_id</code> to query by

  * `[projection]` &lt;[Object][]&gt; optional fields to return (http://bit.ly/1HotzBo)
  * `[options]` &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 参见：

  * [field selection]()

  * [lean queries]()

The id is cast based on the Schema before sending the command.

**This function triggers the following middleware**

  * findOne()


* Except for how it treats undefined. If you use findOne(), you'll see
that findOne(undefined) and findOne({ _id: undefined }) are equivalent
to findOne({}) and return arbitrary documents. However, mongoose
translates findById(undefined) into findOne({ _id: null }).

##### 示例：

```js
// find adventure by id and execute immediately
Adventure.findById(id, function (err, adventure) {});

// same as above
Adventure.findById(id).exec(callback);

// select only the adventures name and length
Adventure.findById(id, 'name length', function (err, adventure) {});

// same as above
Adventure.findById(id, 'name length').exec(callback);

// include all properties except for `length`
Adventure.findById(id, '-length').exec(function (err, adventure) {});

// passing options (in this case return the raw js objects, not mongoose documents by passing `lean`
Adventure.findById(id, 'name', { lean: true }, function (err, doc) {});

// same as above
Adventure.findById(id, 'name').lean().exec(function (err, doc) {});
```


## Model.findByIdAndRemove(id, [options], [callback])

Issue a mongodb findAndModify remove command by a document's _id field. findByIdAndRemove(id, ...) is equivalent to findOneAndRemove({ _id: id }, ...).

<!--sec data-title="源码" data-id="Model_findByIdAndRemove" data-show=true data-collapse=true ces-->
```js
Model.findByIdAndRemove = function(id, options, callback) {
  if (arguments.length === 1 && typeof id === 'function') {
    var msg = 'Model.findByIdAndRemove(): First argument must not be a function.

'
        + '  ' + this.modelName + '.findByIdAndRemove(id, callback)
'
        + '  ' + this.modelName + '.findByIdAndRemove(id)
'
        + '  ' + this.modelName + '.findByIdAndRemove()
';
    throw new TypeError(msg);
  }
  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  return this.findOneAndRemove({_id: id}, options, callback);
};
```
<!--endsec-->

##### 参数：

  * `id` <Object, Number, String> value of <code>_id</code> to query by

  * `[options]` &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 参见：

  * [Model.findOneAndRemove]()

  * [mongodb](http://www.mongodb.org/display/DOCS/findAndModify+Command)

Finds a matching document, removes it, passing the found document (if any) to the callback.

Executes immediately if callback is passed, else a Query object is returned.

**This function triggers the following middleware**

  * findOneAndRemove()

##### 选项：

  * `sort`: if multiple docs are found by the conditions, sets the sort order to choose which doc to update
  * `select`: sets the document fields to return
  * `passRawResult`: if true, passes the raw result from the MongoDB driver as the third callback parameter
  * `strict`: overwrites the schema's strict mode option for this update


##### 示例：

```js
A.findByIdAndRemove(id, options, callback) // executes
A.findByIdAndRemove(id, options)  // return Query
A.findByIdAndRemove(id, callback) // executes
A.findByIdAndRemove(id) // returns Query
A.findByIdAndRemove()           // returns Query
```



## Model.findByIdAndUpdate(id, [update], [options], [callback])

Issues a mongodb findAndModify update command by a document's _id field.
findByIdAndUpdate(id, ...) is equivalent to findOneAndUpdate({ _id: id }, ...).

<!--sec data-title="源码" data-id="Model_findByIdAndUpdate" data-show=true data-collapse=true ces-->
```js
Model.findByIdAndUpdate = function(id, update, options, callback) {
  if (callback) {
    callback = this.$wrapCallback(callback);
  }
  if (arguments.length === 1) {
    if (typeof id === 'function') {
      var msg = 'Model.findByIdAndUpdate(): First argument must not be a function.

'
          + '  ' + this.modelName + '.findByIdAndUpdate(id, callback)
'
          + '  ' + this.modelName + '.findByIdAndUpdate(id)
'
          + '  ' + this.modelName + '.findByIdAndUpdate()
';
      throw new TypeError(msg);
    }
    return this.findOneAndUpdate({_id: id}, undefined);
  }

  // if a model is passed in instead of an id
  if (id instanceof Document) {
    id = id._id;
  }

  return this.findOneAndUpdate.call(this, {_id: id}, update, options, callback);
};
```
<!--endsec-->

##### 参数：

  * `id` <Object, Number, String> value of <code>_id</code> to query by

  * `[update]` &lt;[Object][]&gt;

  * `[options]` &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

<Query>

##### 参见：

  * [Model.findOneAndUpdate]()

  * [mongodb](http://www.mongodb.org/display/DOCS/findAndModify+Command)

Finds a matching document, updates it according to the update arg,
passing any options, and returns the found document (if any) to the
callback. The query executes immediately if callback is passed else a
Query object is returned.

**This function triggers the following middleware**

  * findOneAndUpdate()


##### 选项:

  * `new`: bool - true to return the modified document rather than the original. defaults to false
  * `upsert`: bool - creates the object if it doesn't exist. defaults to false.
  * `runValidators`: if true, runs update validators on this command. Update validators validate the update operation against the model's schema.
  * `setDefaultsOnInsert`: if this and upsert are true, mongoose will apply the defaults specified in the model's schema if a new document is created. This option only works on MongoDB >= 2.4 because it relies on MongoDB's $setOnInsert operator.
  * `sort`: if multiple docs are found by the conditions, sets the sort order to choose which doc to update
  * `select`: sets the document fields to return
  * `passRawResult`: if true, passes the raw result from the MongoDB driver as the third callback parameter
  * `strict`: overwrites the schema's strict mode option for this update
  * `runSettersOnQuery`: bool - if true, run all setters defined on the associated model's schema for all fields defined in the query and the update.
##### 示例：

```js
A.findByIdAndUpdate(id, update, options, callback) // executes
A.findByIdAndUpdate(id, update, options)  // returns Query
A.findByIdAndUpdate(id, update, callback) // executes
A.findByIdAndUpdate(id, update)           // returns Query
A.findByIdAndUpdate()                     // returns Query
```

##### 注意：

All top level update keys which are not atomic operation names are treated as set operations:

##### 示例：

```js
Model.findByIdAndUpdate(id, { name: 'jason bourne' }, options, callback)

// is sent as
Model.findByIdAndUpdate(id, { $set: { name: 'jason bourne' }}, options, callback)
```

This helps prevent accidentally overwriting your document with { name: 'jason bourne' }.

##### 注意：

Values are cast to their appropriate types when using the findAndModify helpers.
However, the below are not executed by default.

* defaults. Use the setDefaultsOnInsert option to override.
* setters. Use the runSettersOnQuery option to override.


findAndModify helpers support limited validation. You can
enable these by setting the runValidators options,
respectively.

If you need full-fledged validation, use the traditional approach of first
retrieving the document.

```js
Model.findById(id, function (err, doc) {
  if (err) ..
  doc.name = 'jason bourne';
  doc.save(callback);
});
```


## Model.findOne([conditions], [projection], [options], [callback])

Finds one document.

<!--sec data-title="源码" data-id="Model_findOne" data-show=true data-collapse=true ces-->
```js
Model.findOne = function findOne(conditions, projection, options, callback) {
  if (typeof options === 'function') {
    callback = options;
    options = null;
  } else if (typeof projection === 'function') {
    callback = projection;
    projection = null;
    options = null;
  } else if (typeof conditions === 'function') {
    callback = conditions;
    conditions = {};
    projection = null;
    options = null;
  }

  // get the mongodb collection object
  var mq = new this.Query({}, {}, this, this.collection);
  mq.select(projection);
  mq.setOptions(options);
  if (this.schema.discriminatorMapping &&
      this.schema.discriminatorMapping.isRoot &&
      mq.selectedInclusively()) {
    mq.select(this.schema.options.discriminatorKey);
  }

  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  return mq.findOne(conditions, callback);
};
```
<!--endsec-->

##### 参数：

  * `[conditions]` &lt;[Object][]&gt;
  * `[projection]` &lt;[Object][]&gt; optional fields to return (http://bit.ly/1HotzBo)

  * `[options]` &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 参见：

  * [field selection]()

  * [lean queries]()

The conditions are cast to their respective SchemaTypes before the command is sent.

##### 注意：

 conditions is optional, and if conditions is null or undefined,
mongoose will send an empty findOne command to MongoDB, which will return
an arbitrary document. If you're querying by _id, use findById() instead.

##### 示例：

```js
// find one iphone adventures - iphone adventures??
Adventure.findOne({ type: 'iphone' }, function (err, adventure) {});

// same as above
Adventure.findOne({ type: 'iphone' }).exec(function (err, adventure) {});

// select only the adventures name
Adventure.findOne({ type: 'iphone' }, 'name', function (err, adventure) {});

// same as above
Adventure.findOne({ type: 'iphone' }, 'name').exec(function (err, adventure) {});

// specify options, in this case lean
Adventure.findOne({ type: 'iphone' }, 'name', { lean: true }, callback);

// same as above
Adventure.findOne({ type: 'iphone' }, 'name', { lean: true }).exec(callback);

// chaining findOne queries (same as above)
Adventure.findOne({ type: 'iphone' }).select('name').lean().exec(callback);
```



## Model.findOneAndRemove(conditions, [options], [callback])

Issue a mongodb findAndModify remove command.

<!--sec data-title="源码" data-id="Model_findOneAndRemove" data-show=true data-collapse=true ces-->
```js
Model.findOneAndRemove = function(conditions, options, callback) {
  if (arguments.length === 1 && typeof conditions === 'function') {
    var msg = 'Model.findOneAndRemove(): First argument must not be a function.

'
        + '  ' + this.modelName + '.findOneAndRemove(conditions, callback)
'
        + '  ' + this.modelName + '.findOneAndRemove(conditions)
'
        + '  ' + this.modelName + '.findOneAndRemove()
';
    throw new TypeError(msg);
  }

  if (typeof options === 'function') {
    callback = options;
    options = undefined;
  }
  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  var fields;
  if (options) {
    fields = options.select;
    options.select = undefined;
  }

  var mq = new this.Query({}, {}, this, this.collection);
  mq.select(fields);

  return mq.findOneAndRemove(conditions, options, callback);
};
```
<!--endsec-->

##### 参数：

  * `conditions` &lt;[Object][]&gt;

  * `[options]` &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 参见：

  * [mongodb](http://www.mongodb.org/display/DOCS/findAndModify+Command)

Finds a matching document, removes it, passing the found document (if any) to the callback.

Executes immediately if callback is passed else a Query object is returned.

**This function triggers the following middleware**

  * findOneAndRemove()


##### 选项:

  * `sort`: if multiple docs are found by the conditions, sets the sort order to choose which doc to update
  * `maxTimeMS`: puts a time limit on the query - requires mongodb >= 2.6.0
  * `select`: sets the document fields to return
  * `passRawResult`: if true, passes the raw result from the MongoDB driver as the third callback parameter
  * `strict`: overwrites the schema's strict mode option for this update

##### 示例：

```js
A.findOneAndRemove(conditions, options, callback) // executes
A.findOneAndRemove(conditions, options)  // return Query
A.findOneAndRemove(conditions, callback) // executes
A.findOneAndRemove(conditions) // returns Query
A.findOneAndRemove()           // returns Query
```

Values are cast to their appropriate types when using the findAndModify helpers.
However, the below are not executed by default.

* defaults. Use the setDefaultsOnInsert option to override.
* setters. Use the runSettersOnQuery option to override.


findAndModify helpers support limited validation. You can
enable these by setting the runValidators options,
respectively.

If you need full-fledged validation, use the traditional approach of first
retrieving the document.

```js
Model.findById(id, function (err, doc) {
  if (err) ..
  doc.name = 'jason bourne';
  doc.save(callback);
});
```


## Model.findOneAndUpdate([conditions], [update], [options], [callback])

Issues a mongodb findAndModify update command.

<!--sec data-title="源码" data-id="Model_findOneAndUpdate" data-show=true data-collapse=true ces-->
```js
Model.findOneAndUpdate = function(conditions, update, options, callback) {
  if (typeof options === 'function') {
    callback = options;
    options = null;
  } else if (arguments.length === 1) {
    if (typeof conditions === 'function') {
      var msg = 'Model.findOneAndUpdate(): First argument must not be a function.

'
          + '  ' + this.modelName + '.findOneAndUpdate(conditions, update, options, callback)
'
          + '  ' + this.modelName + '.findOneAndUpdate(conditions, update, options)
'
          + '  ' + this.modelName + '.findOneAndUpdate(conditions, update)
'
          + '  ' + this.modelName + '.findOneAndUpdate(update)
'
          + '  ' + this.modelName + '.findOneAndUpdate()
';
      throw new TypeError(msg);
    }
    update = conditions;
    conditions = undefined;
  }
  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  var fields;
  if (options && options.fields) {
    fields = options.fields;
  }

  update = utils.clone(update, {depopulate: 1, _isNested: true});
  if (this.schema.options.versionKey && options && options.upsert) {
    if (options.overwrite) {
      update[this.schema.options.versionKey] = 0;
    } else {
      if (!update.$setOnInsert) {
        update.$setOnInsert = {};
      }
      update.$setOnInsert[this.schema.options.versionKey] = 0;
    }
  }

  var mq = new this.Query({}, {}, this, this.collection);
  mq.select(fields);

  return mq.findOneAndUpdate(conditions, update, options, callback);
};
```
<!--endsec-->

##### 参数：

  * `[conditions]` &lt;[Object][]&gt;

  * `[update]` &lt;[Object][]&gt;

  * `[options]` &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 参见：

  * [mongodb](http://www.mongodb.org/display/DOCS/findAndModify+Command)

Finds a matching document, updates it according to the update arg, passing any options, and returns the found document (if any) to the callback. The query executes immediately if callback is passed else a Query object is returned.

##### 选项:

  * `new`: bool - if true, return the modified document rather than the original. defaults to false (changed in 4.0)
  * `upsert`: bool - creates the object if it doesn't exist. defaults to false.
  * `fields`: {Object|String} - Field selection. Equivalent to .select(fields).findOneAndUpdate()
  * `maxTimeMS`: puts a time limit on the query - requires mongodb >= 2.6.0
  * `sort`: if multiple docs are found by the conditions, sets the sort order to choose which doc to update
  * `runValidators`: if true, runs update validators on this command. Update validators validate the update operation against the model's schema.
  * `setDefaultsOnInsert`: if this and upsert are true, mongoose will apply the defaults specified in the model's schema if a new document is created. This option only works on MongoDB >= 2.4 because it relies on MongoDB's $setOnInsert operator.
  * `passRawResult`: if true, passes the raw result from the MongoDB driver as the third callback parameter
  * `strict`: overwrites the schema's strict mode option for this update
  * `runSettersOnQuery`: bool - if true, run all setters defined on the associated model's schema for all fields defined in the query and the update.


##### 示例：

```js
A.findOneAndUpdate(conditions, update, options, callback) // executes
A.findOneAndUpdate(conditions, update, options)  // returns Query
A.findOneAndUpdate(conditions, update, callback) // executes
A.findOneAndUpdate(conditions, update)           // returns Query
A.findOneAndUpdate()                             // returns Query

```

##### 注意：

All top level update keys which are not atomic operation names are treated as set operations:

##### 示例：

```js
var query = { name: 'borne' };
Model.findOneAndUpdate(query, { name: 'jason bourne' }, options, callback)

// is sent as
Model.findOneAndUpdate(query, { $set: { name: 'jason bourne' }}, options, callback)
```

This helps prevent accidentally overwriting your document with { name: 'jason bourne' }.

##### 注意：

Values are cast to their appropriate types when using the findAndModify helpers.
However, the below are not executed by default.

* defaults. Use the setDefaultsOnInsert option to override.
* setters. Use the runSettersOnQuery option to override.


findAndModify helpers support limited validation. You can
enable these by setting the runValidators options,
respectively.

If you need full-fledged validation, use the traditional approach of first
retrieving the document.

```js
Model.findById(id, function (err, doc) {
  if (err) ..
  doc.name = 'jason bourne';
  doc.save(callback);
});
```


## Model.geoNear(GeoJSON, options, [callback])

geoNear support for Mongoose

<!--sec data-title="源码" data-id="Model_geoNear" data-show=true data-collapse=true ces-->
```js
Model.geoNear = function(near, options, callback) {
  if (typeof options === 'function') {
    callback = options;
    options = {};
  }

  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  var _this = this;
  var Promise = PromiseProvider.get();
  if (!near) {
    return new Promise.ES6(function(resolve, reject) {
      var error = new Error('Must pass a near option to geoNear');
      reject(error);
      callback && callback(error);
    });
  }

  var x;
  var y;
  var schema = this.schema;

  return new Promise.ES6(function(resolve, reject) {
    var handler = function(err, res) {
      if (err) {
        reject(err);
        callback && callback(err);
        return;
      }
      if (options.lean) {
        resolve(res.results, res.stats);
        callback && callback(null, res.results, res.stats);
        return;
      }

      var count = res.results.length;
      // if there are no results, fulfill the promise now
      if (count === 0) {
        resolve(res.results, res.stats);
        callback && callback(null, res.results, res.stats);
        return;
      }

      var errSeen = false;

      function init(err) {
        if (err && !errSeen) {
          errSeen = true;
          reject(err);
          callback && callback(err);
          return;
        }
        if (--count <= 0) {
          resolve(res.results, res.stats);
          callback && callback(null, res.results, res.stats);
        }
      }

      for (var i = 0; i < res.results.length; i++) {
        var temp = res.results[i].obj;
        res.results[i].obj = new _this();
        res.results[i].obj.init(temp, init);
      }
    };

    if (options.query != null) {
      options.query = utils.clone(options.query, { retainKeyOrder: 1 });
      cast(schema, options.query);
    }

    if (Array.isArray(near)) {
      if (near.length !== 2) {
        var error = new Error('If using legacy coordinates, must be an array ' +
            'of size 2 for geoNear');
        reject(error);
        callback && callback(error);
        return;
      }
      x = near[0];
      y = near[1];
      _this.collection.geoNear(x, y, options, handler);
    } else {
      if (near.type !== 'Point' || !Array.isArray(near.coordinates)) {
        error = new Error('Must pass either a legacy coordinate array or ' +
            'GeoJSON Point to geoNear');
        reject(error);
        callback && callback(error);
        return;
      }

      _this.collection.geoNear(near, options, handler);
    }
  });
};
```
<!--endsec-->

##### 参数：

  * `GeoJSON` <Object, Array> point or legacy coordinate pair [x,y] to search near

  * `options` &lt;[Object][]&gt; for the query

  * [callback] &lt;[Function][]&gt; optional callback for the query

##### 返回值：

  * <Promise>

##### 参见：

  * http://docs.mongodb.org/manual/core/2dsphere/

  * http://mongodb.github.io/node-mongodb-native/api-generated/collection.html?highlight=geonear#geoNear

This function does not trigger any middleware. In particular, this
bypasses find() middleware.

##### 选项:

lean {Boolean} return the raw object
All options supported by the driver are also supported

##### 示例：

```js
// Legacy point
Model.geoNear([1,3], { maxDistance : 5, spherical : true }, function(err, results, stats) {
   console.log(results);
});

// geoJson
var point = { type : "Point", coordinates : [9,9] };
Model.geoNear(point, { maxDistance : 5, spherical : true }, function(err, results, stats) {
   console.log(results);
});
```



## Model.geoSearch(conditions, options, [callback])

Implements $geoSearch functionality for Mongoose

<!--sec data-title="源码" data-id="Model_geoSearch" data-show=true data-collapse=true ces-->
```js
Model.geoSearch = function(conditions, options, callback) {
  if (typeof options === 'function') {
    callback = options;
    options = {};
  }
  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  var _this = this;
  var Promise = PromiseProvider.get();
  return new Promise.ES6(function(resolve, reject) {
    var error;
    if (conditions === undefined || !utils.isObject(conditions)) {
      error = new Error('Must pass conditions to geoSearch');
    } else if (!options.near) {
      error = new Error('Must specify the near option in geoSearch');
    } else if (!Array.isArray(options.near)) {
      error = new Error('near option must be an array [x, y]');
    }

    if (error) {
      callback && callback(error);
      reject(error);
      return;
    }

    // send the conditions in the options object
    options.search = conditions;

    _this.collection.geoHaystackSearch(options.near[0], options.near[1], options, function(err, res) {
      // have to deal with driver problem. Should be fixed in a soon-ish release
      // (7/8/2013)
      if (err) {
        callback && callback(err);
        reject(err);
        return;
      }

      var count = res.results.length;
      if (options.lean || count === 0) {
        callback && callback(null, res.results, res.stats);
        resolve(res.results, res.stats);
        return;
      }

      var errSeen = false;

      function init(err) {
        if (err && !errSeen) {
          callback && callback(err);
          reject(err);
          return;
        }

        if (!--count && !errSeen) {
          callback && callback(null, res.results, res.stats);
          resolve(res.results, res.stats);
        }
      }

      for (var i = 0; i < res.results.length; i++) {
        var temp = res.results[i];
        res.results[i] = new _this();
        res.results[i].init(temp, {}, init);
      }
    });
  });
};

```
<!--endsec-->

##### 参数：

  * `conditions` &lt;[Object][]&gt; an object that specifies the match condition (required)

  * `options` &lt;[Object][]&gt; for the geoSearch, some (near, maxDistance) are required

  * `[callback]` &lt;[Function][]&gt; optional callback

##### 返回值：

  * <Promise>

##### 参见：

  * http://docs.mongodb.org/manual/reference/command/geoSearch/

  * http://docs.mongodb.org/manual/core/geohaystack/

This function does not trigger any middleware

##### 示例：

```js
var options = { near: [10, 10], maxDistance: 5 };
Locations.geoSearch({ type : "house" }, options, function(err, res) {
  console.log(res);
});
```

##### 选项:

  * `near` {Array} x,y point to search for
  * `maxDistance` {Number} the maximum distance from the point near that a result can be
  * `limit` {Number} The maximum number of results to return
  * `lean` {Boolean} return the raw object instead of the Mongoose Model


## Model.hydrate(obj)

Shortcut for creating a new Document from existing raw data, pre-saved in the DB.
The document returned has no paths marked as modified initially.

<!--sec data-title="源码" data-id="Model_hydrate" data-show=true data-collapse=true ces-->
```js
Model.hydrate = function(obj) {
  var model = require('./queryhelpers').createModel(this, obj);
  model.init(obj);
  return model;
};
```
<!--endsec-->

##### 参数：

  * `obj` &lt;[Object][]&gt;

##### 返回值：

  * <Document>

##### 示例：

```js
// hydrate previous data into a Mongoose document
var mongooseCandy = Candy.hydrate({ _id: '54108337212ffb6d459f854c', type: 'jelly bean' });
```



## Model.init([callback])

Performs any async initialization of this model against MongoDB. Currently,
this function is only responsible for building [indexes](https://docs.mongodb.com/manual/indexes/),
unless [autoIndex]() is turned off.

<!--sec data-title="源码" data-id="Model_init" data-show=true data-collapse=true ces-->
```js
Model.init = function init(callback) {
  this.schema.emit('init', this);

  if (this.$init) {
    return this.$init;
  }

  var _this = this;
  var Promise = PromiseProvider.get();
  this.$init = new Promise.ES6(function(resolve, reject) {
    if ((_this.schema.options.autoIndex) ||
        (_this.schema.options.autoIndex == null && _this.db.config.autoIndex)) {
      _this.ensureIndexes({ _automatic: true, __noPromise: true }, function(error) {
        if (error) {
          callback && callback(error);
          return reject(error);
        }
        callback && callback(null, _this);
        resolve(_this);
      });
    } else {
      resolve(_this);
    }
  });

  return this.$init;
};

```
<!--endsec-->

##### 参数：

  * `[callback]` &lt;[Function][]&gt;

This function is called automatically, so you don't need to call it.
This function is also idempotent, so you may call it to get back a promise
that will resolve when your indexes are finished building as an alternative
to MyModel.on('index')

##### 示例：

```js
var eventSchema = new Schema({ thing: { type: 'string', unique: true }})
// This calls `Event.init()` implicitly, so you don't need to call
// `Event.init()` on your own.
var Event = mongoose.model('Event', eventSchema);

Event.init().then(function(Event) {
  // You can also use `Event.on('index')` if you prefer event emitters
  // over promises.
  console.log('Indexes are done building!');
});
```



## Model.insertMany(doc(s), [options], [options.ordered, [options.rawResult, [callback])


Shortcut for validating an array of documents and inserting them into
MongoDB if they're all valid. This function is faster than .create()
because it only sends one operation to the server, rather than one for each
document.

<!--sec data-title="源码" data-id="Model_insertMany" data-show=true data-collapse=true ces-->
```js
Model.insertMany = function(arr, options, callback) {
  var _this = this;
  if (typeof options === 'function') {
    callback = options;
    options = null;
  }
  if (callback) {
    callback = this.$wrapCallback(callback);
  }
  callback = callback || utils.noop;
  options = options || {};
  var limit = get(options, 'limit', 1000);
  var rawResult = get(options, 'rawResult', false);
  var ordered = get(options, 'ordered', true);

  if (!Array.isArray(arr)) {
    arr = [arr];
  }

  var toExecute = [];
  var validationErrors = [];
  arr.forEach(function(doc) {
    toExecute.push(function(callback) {
      doc = new _this(doc);
      doc.validate({ __noPromise: true }, function(error) {
        if (error) {
          // Option `ordered` signals that insert should be continued after reaching
          // a failing insert. Therefore we delegate "null", meaning the validation
          // failed. It's up to the next function to filter out all failed models
          if (ordered === false) {
            validationErrors.push(error);
            return callback(null, null);
          }
          return callback(error);
        }
        callback(null, doc);
      });
    });
  });

  parallelLimit(toExecute, limit, function(error, docs) {
    if (error) {
      callback && callback(error);
      return;
    }
    // We filter all failed pre-validations by removing nulls
    var docAttributes = docs.filter(function(doc) {
      return doc != null;
    });
    // Quickly escape while there aren't any valid docAttributes
    if (docAttributes.length < 1) {
      callback(null, []);
      return;
    }
    var docObjects = docAttributes.map(function(doc) {
      if (doc.schema.options.versionKey) {
        doc[doc.schema.options.versionKey] = 0;
      }
      if (doc.initializeTimestamps) {
        return doc.initializeTimestamps().toObject(INSERT_MANY_CONVERT_OPTIONS);
      }
      return doc.toObject(INSERT_MANY_CONVERT_OPTIONS);
    });

    _this.collection.insertMany(docObjects, options, function(error, res) {
      if (error) {
        callback && callback(error);
        return;
      }
      for (var i = 0; i < docAttributes.length; ++i) {
        docAttributes[i].isNew = false;
        docAttributes[i].emit('isNew', false);
        docAttributes[i].constructor.emit('isNew', false);
      }
      if (rawResult) {
        if (ordered === false) {
          // Decorate with mongoose validation errors in case of unordered,
          // because then still do `insertMany()`
          res.mongoose = {
            validationErrors: validationErrors
          };
        }
        return callback(null, res);
      }
      callback(null, docAttributes);
    });
  });
};
```
<!--endsec-->
##### 参数：

doc(s) <Array, Object, *>

  * `[options]` &lt;[Object][]&gt; see the <a href="http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#insertMany">mongodb driver options</a>

  * `[options.ordered &lt;[Boolean][]&gt; = true]` if true, will fail fast on the first error encountered. If false, will insert all the documents it can and report errors later. An <code>insertMany()</code> with <code>ordered = false</code> is called an "unordered" <code>insertMany()</code>.

  * `[options.rawResult &lt;[Boolean][]&gt; = false]` if false, the returned promise resolves to the documents that passed mongoose document validation. If <code>false</code>, will return the <a href="http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#~insertWriteOpCallback">raw result from the MongoDB driver</a> with a <code>mongoose</code> property that contains <code>validationErrors</code> if this is an unordered <code>insertMany</code>.

  * `[callback]` &lt;[Function][]&gt; callback

##### 返回值：

  * <Promise>

Mongoose always validates each document before sending insertMany
to MongoDB. So if one document has a validation error, no documents will
be saved, unless you set
[the ordered option to false.](https://docs.mongodb.com/manual/reference/method/db.collection.insertMany/#error-handling)

This function does **not** trigger save middleware.

**This function triggers the following middleware**

  * insertMany()


##### 示例：

```js
var arr = [{ name: 'Star Wars' }, { name: 'The Empire Strikes Back' }];
Movies.insertMany(arr, function(error, docs) {});
```


## Model.mapReduce(o, [callback])

Executes a mapReduce command.

<!--sec data-title="源码" data-id="Model_mapReduce" data-show=true data-collapse=true ces-->
```js
Model.mapReduce = function mapReduce(o, callback) {
  var _this = this;
  if (callback) {
    callback = this.$wrapCallback(callback);
  }
  var resolveToObject = o.resolveToObject;
  var Promise = PromiseProvider.get();
  return new Promise.ES6(function(resolve, reject) {
    if (!Model.mapReduce.schema) {
      var opts = {noId: true, noVirtualId: true, strict: false};
      Model.mapReduce.schema = new Schema({}, opts);
    }

    if (!o.out) o.out = {inline: 1};
    if (o.verbose !== false) o.verbose = true;

    o.map = String(o.map);
    o.reduce = String(o.reduce);

    if (o.query) {
      var q = new _this.Query(o.query);
      q.cast(_this);
      o.query = q._conditions;
      q = undefined;
    }

    _this.collection.mapReduce(null, null, o, function(err, ret, stats) {
      if (err) {
        callback && callback(err);
        reject(err);
        return;
      }

      if (ret.findOne && ret.mapReduce) {
        // returned a collection, convert to Model
        var model = Model.compile(
            '_mapreduce_' + ret.collectionName
            , Model.mapReduce.schema
            , ret.collectionName
            , _this.db
            , _this.base);

        model._mapreduce = true;

        callback && callback(null, model, stats);
        return resolveToObject ? resolve({
          model: model,
          stats: stats
        }) : resolve(model, stats);
      }

      callback && callback(null, ret, stats);
      if (resolveToObject) {
        return resolve({ model: ret, stats: stats });
      }
      resolve(ret, stats);
    });
  });
};
```
<!--endsec-->

##### 参数：

  * `o` &lt;[Object][]&gt; an object specifying map-reduce options

  * `[callback]` &lt;[Function][]&gt; optional callback

##### 返回值：

  * <Promise>

##### 参见：

  * http://www.mongodb.org/display/DOCS/MapReduce

o is an object specifying all mapReduce options as well as the map and reduce functions. All options are delegated to the driver implementation. See node-mongodb-native mapReduce() documentation for more detail about options.

This function does **not** trigger any middleware.

##### 示例：

```js
var o = {};
o.map = function () { emit(this.name, 1) }
o.reduce = function (k, vals) { return vals.length }
User.mapReduce(o, function (err, results) {
  console.log(results)
})
```

##### 其他选项:

  * `query` {Object} query filter object.
  * `sort` {Object} sort input objects using this key
  * `limit` {Number} max number of documents
  * `keeptemp` {Boolean, default:false} keep temporary data
  * `finalize` {Function} finalize function
  * `scope` {Object} scope variables exposed to map/reduce/finalize during execution
  * `jsMode` {Boolean, default:false} it is possible to make the execution stay in JS. Provided in MongoDB > 2.0.X
  * `verbose` {Boolean, default:false} provide statistics on job execution time.
  * `readPreference` {String}
  * `out*` {Object, default: {inline:1}} sets the output target for the map reduce job.
    out 选项:
      - `{inline:1}` the results are returned in an array
      - `{replace: 'collectionName'}` add the results to collectionName: the results replace the collection
      - `{reduce: 'collectionName'}` add the results to collectionName: if dups are detected, uses the reducer / finalize functions
      - `{merge: 'collectionName'}` add the results to collectionName: if dups exist the new docs overwrite the old


If options.out is set to replace, merge, or reduce, a Model instance is returned that can be used for further querying. Queries run against this model are all executed with the lean option; meaning only the js object is returned and no Mongoose magic is applied (getters, setters, etc).

##### 示例：

```js
var o = {};
o.map = function () { emit(this.name, 1) }
o.reduce = function (k, vals) { return vals.length }
o.out = { replace: 'createdCollectionNameForResults' }
o.verbose = true;

User.mapReduce(o, function (err, model, stats) {
  console.log('map reduce took %d ms', stats.processtime)
  model.find().where('value').gt(10).exec(function (err, docs) {
    console.log(docs);
  });
})

// `mapReduce()` returns a promise. However, ES6 promises can only
// resolve to exactly one value,
o.resolveToObject = true;
var promise = User.mapReduce(o);
promise.then(function (res) {
  var model = res.model;
  var stats = res.stats;
  console.log('map reduce took %d ms', stats.processtime)
  return model.find().where('value').gt(10).exec();
}).then(function (docs) {
   console.log(docs);
}).then(null, handleError).end()
```



## Model.populate(docs, options, [callback(err,doc)])

Populates document references.

<!--sec data-title="源码" data-id="Model_populate" data-show=true data-collapse=true ces-->
```js
Model.populate = function(docs, paths, callback) {
  var _this = this;
  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  // normalized paths
  var noPromise = paths && !!paths.__noPromise;
  paths = utils.populate(paths);

  // data that should persist across subPopulate calls
  var cache = {};

  if (noPromise) {
    _populate(this, docs, paths, cache, callback);
  } else {
    var Promise = PromiseProvider.get();
    return new Promise.ES6(function(resolve, reject) {
      _populate(_this, docs, paths, cache, function(error, docs) {
        if (error) {
          callback && callback(error);
          reject(error);
        } else {
          callback && callback(null, docs);
          resolve(docs);
        }
      });
    });
  }
};
```
<!--endsec-->

##### 参数：

  * `docs` <Document, Array> Either a single document or array of documents to populate.

  * `options` &lt;[Object][]&gt; A hash of key/val (path, options) used for population.

  * `[callback(err,doc)]` &lt;[Function][]&gt; Optional callback, executed upon completion. Receives <code>err</code> and the <code>doc(s)</code>.

##### 返回值：

  * <Promise>

可用选项:

  * `path`: space delimited path(s) to populate
  * `select`: optional fields to select
  * `match`: optional query conditions to match
  * `model`: optional name of the model to use for population
  * `options`: optional query options like sort, limit, etc


##### 示例：

```js
// populates a single object
User.findById(id, function (err, user) {
  var opts = [
      { path: 'company', match: { x: 1 }, select: 'name' }
    , { path: 'notes', options: { limit: 10 }, model: 'override' }
  ]

  User.populate(user, opts, function (err, user) {
    console.log(user);
  });
});

// populates an array of objects
User.find(match, function (err, users) {
  var opts = [{ path: 'company', match: { x: 1 }, select: 'name' }]

  var promise = User.populate(users, opts);
  promise.then(console.log).end();
})

// imagine a Weapon model exists with two saved documents:
//   { _id: 389, name: 'whip' }
//   { _id: 8921, name: 'boomerang' }
// and this schema:
// new Schema({
//   name: String,
//   weapon: { type: ObjectId, ref: 'Weapon' }
// });

var user = { name: 'Indiana Jones', weapon: 389 }
Weapon.populate(user, { path: 'weapon', model: 'Weapon' }, function (err, user) {
  console.log(user.weapon.name) // whip
})

// populate many plain objects
var users = [{ name: 'Indiana Jones', weapon: 389 }]
users.push({ name: 'Batman', weapon: 8921 })
Weapon.populate(users, { path: 'weapon' }, function (err, users) {
  users.forEach(function (user) {
    console.log('%s uses a %s', users.name, user.weapon.name)
    // Indiana Jones uses a whip
    // Batman uses a boomerang
  });
});
// Note that we didn't need to specify the Weapon model because
// it is in the schema's ref

```



## Model.remove(conditions, [callback])

Removes all documents that match conditions from the collection.
To remove just the first document that matches conditions, set the single
option to true.

<!--sec data-title="源码" data-id="Model_remove_" data-show=true data-collapse=true ces-->
```js
Model.remove = function remove(conditions, callback) {
  if (typeof conditions === 'function') {
    callback = conditions;
    conditions = {};
  }

  // get the mongodb collection object
  var mq = new this.Query({}, {}, this, this.collection);

  if (callback) {
    callback = this.$wrapCallback(callback);
  }

  return mq.remove(conditions, callback);
};
```
<!--endsec-->

##### 参数：

  * `conditions` &lt;[Object][]&gt;

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 示例：

```js
Character.remove({ name: 'Eddard Stark' }, function (err) {});
```

##### 注意：

This method sends a remove command directly to MongoDB, no Mongoose documents
are involved. Because no Mongoose documents are involved, no middleware
(hooks) are executed.



## Model.replaceOne(conditions, doc, [options], [callback])

Same as update(), except MongoDB replace the existing document with the
given document (no atomic operators like $set).

<!--sec data-title="源码" data-id="Model_replaceOne" data-show=true data-collapse=true ces-->
```js
Model.replaceOne = function replaceOne(conditions, doc, options, callback) {
  return _update(this, 'replaceOne', conditions, doc, options, callback);
};
```
<!--endsec-->

##### 参数：

  * `conditions` &lt;[Object][]&gt;

  * `doc` &lt;[Object][]&gt;

  * `[options]` &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

**This function triggers the following middleware**

  * replaceOne()



## Model.translateAliases(raw)

Translate any aliases fields/conditions so the final query or document object is pure

<!--sec data-title="源码" data-id="Model_translateAliases" data-show=true data-collapse=true ces-->
```js
Model.translateAliases = function translateAliases(fields) {
  var aliases = this.schema.aliases;

  if (typeof fields === 'object') {
    // Fields is an object (query conditions or document fields)
    for (var key in fields) {
      if (aliases[key]) {
        fields[aliases[key]] = fields[key];
        delete fields[key];
      }
    }

    return fields;
  } else {
    // Don't know typeof fields
    return fields;
  }
};
```
<!--endsec-->

##### 参数：

  * `raw` &lt;[Object][]&gt; fields/conditions that may contain aliased keys

##### 返回值：

  * &lt;[Object][]&gt; the translated 'pure' fields/conditions

##### 示例：

```js
Character
  .find(Character.translateAliases({
    '名': 'Eddard Stark' // Alias for 'name'
  }))
  .exec(function(err, characters) {})
```

##### 注意：

Only translate arguments of object type anything else is returned raw



## Model.update(conditions, doc, [options], [callback])

Updates one document in the database without returning it.

<!--sec data-title="源码" data-id="Model_update" data-show=true data-collapse=true ces-->
```js
Model.update = function update(conditions, doc, options, callback) {
  return _update(this, 'update', conditions, doc, options, callback);
};
```
<!--endsec-->

##### 参数：

conditions &lt;[Object][]&gt;

doc &lt;[Object][]&gt;

[options] &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

    * `[callback]` &lt;[Function][]&gt;

##### 返回值：

    * <Query>

##### 参见：

    * `strict`

    * `response`

**This function triggers the following middleware**

    * update()

##### 示例：

```js
MyModel.update({ age: { $gt: 18 } }, { oldEnough: true }, fn);
MyModel.update({ name: 'Tobi' }, { ferret: true }, { multi: true }, function (err, raw) {
  if (err) return handleError(err);
  console.log('The raw response from Mongo was ', raw);
});
```

##### 可用选项：

  * `safe` (boolean) safe mode (defaults to value set in schema (true))
  * `upsert` (boolean) whether to create the doc if it doesn't match (false)
  * `multi` (boolean) whether multiple documents should be updated (false)
  * `runValidators`: if true, runs update validators on this command. Update validators validate the update operation against the model's schema.
  * `setDefaultsOnInsert`: if this and upsert are true, mongoose will apply the defaults specified in the model's schema if a new document is created. This option only works on MongoDB >= 2.4 because it relies on MongoDB's $setOnInsert operator.
  * `strict` (boolean) overrides the strict option for this update
  * `overwrite` (boolean) disables update-only mode, allowing you to overwrite the doc (false)


All update values are cast to their appropriate SchemaTypes before being sent.

The callback function receives (err, rawResponse).

  * err is the error if any occurred
  * rawResponse is the full response from Mongo
  *
##### 注意：

All top level keys which are not atomic operation names are treated as set operations:

##### 示例：

```js
var query = { name: 'borne' };
Model.update(query, { name: 'jason bourne' }, options, callback)

// is sent as
Model.update(query, { $set: { name: 'jason bourne' }}, options, callback)
// if overwrite option is false. If overwrite is true, sent without the $set wrapper.
```

This helps prevent accidentally overwriting all documents in your collection with { name: 'jason bourne' }.

##### 注意：

Be careful to not use an existing model instance for the update clause (this won't work and can cause weird behavior like infinite loops). Also, ensure that the update clause does not have an _id property, which causes Mongo to return a "Mod on _id not allowed" error.

##### 注意：

To update documents without waiting for a response from MongoDB, do not pass a callback, then call exec on the returned Query:

```js
Comment.update({ _id: id }, { $set: { text: 'changed' }}).exec();
```

##### 注意：

Although values are casted to their appropriate types when using update, the following are not applied:

  * defaults
  * setters
  * validators
  * middleware
If you need those features, use the traditional approach of first retrieving the document.

```js
Model.findOne({ name: 'borne' }, function (err, doc) {
  if (err) ..
  doc.name = 'jason bourne';
  doc.save(callback);
})
```



## Model.updateMany(conditions, doc, [options], [callback])

Same as update(), except MongoDB will update all documents that match
criteria (as opposed to just the first one) regardless of the value of
the multi option.

<!--sec data-title="源码" data-id="Model_updateMany" data-show=true data-collapse=true ces-->
```js
Model.updateMany = function updateMany(conditions, doc, options, callback) {
  return _update(this, 'updateMany', conditions, doc, options, callback);
};
```
<!--endsec-->

##### 参数：

  * `conditions` &lt;[Object][]&gt;

  * `doc` &lt;[Object][]&gt;

  * `[options]` &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

##### 注意：

updateMany will not fire update middleware. Use pre('updateMany')
and post('updateMany') instead.


**This function triggers the following middleware**

  * updateMany()



## Model.updateOne(conditions, doc, [options], [callback])

Same as update(), except MongoDB will update only the first document that
matches criteria regardless of the value of the multi option.

<!--sec data-title="源码" data-id="Model_updateOne" data-show=true data-collapse=true ces-->
```js
Model.updateOne = function updateOne(conditions, doc, options, callback) {
  return _update(this, 'updateOne', conditions, doc, options, callback);
};
```
<!--endsec-->

##### 参数：

  * `conditions` &lt;[Object][]&gt;

  * `doc` &lt;[Object][]&gt;

  * `[options]` &lt;[Object][]&gt; optional see <a href="http://mongoosejs.com/docs/api.html#query_Query-setOptions"><code>Query.prototype.setOptions()</code></a>

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <Query>

**This function triggers the following middleware**

  * updateOne()


## Model.where(path, [val])

Creates a Query, applies the passed conditions, and returns the Query.

<!--sec data-title="源码" data-id="Model_where_" data-show=true data-collapse=true ces-->
```js
Model.where = function where(path, val) {
  void val; // eslint
  // get the mongodb collection object
  var mq = new this.Query({}, {}, this, this.collection).find({});
  return mq.where.apply(mq, arguments);
};
```
<!--endsec-->

##### 参数：

  * `path` &lt;[String][]&gt;

  * `[val]` &lt;[Object][]&gt; optional value

##### 返回值：

  * <Query>

For example, instead of writing:

```js
User.find({age: {$gte: 21, $lte: 65}}, callback);
```

we can instead write:

```js
User.where('age').gte(21).lte(65).exec(callback);
```

Since the Query class also supports where you can continue chaining

```js
User
.where('age').gte(21).lte(65)
.where('name', /^b/i)
... etc
```


## Model#$where

Additional properties to attach to the query when calling save() and
isNew is false.

<!--sec data-title="源码" data-id="Model_where" data-show=true data-collapse=true ces-->
```js
Model.prototype.$where;
```
<!--endsec-->


## Model#base

Base Mongoose instance the model uses.

<!--sec data-title="源码" data-id="Model_base" data-show=true data-collapse=true ces-->
```js
Model.base;
```
<!--endsec-->


## Model#baseModelName

If this is a discriminator model, baseModelName is the name of
the base model.

<!--sec data-title="源码" data-id="Model_baseModelName" data-show=true data-collapse=true ces-->
```js
Model.prototype.baseModelName;

Model.prototype.$__handleSave = function(options, callback) {
  var _this = this;
  var i;
  var keys;
  var len;
  if (!options.safe && this.schema.options.safe) {
    options.safe = this.schema.options.safe;
  }
  if (typeof options.safe === 'boolean') {
    options.safe = null;
  }
  var safe = options.safe ? utils.clone(options.safe, { retainKeyOrder: true }) : options.safe;

  if (this.isNew) {
    // send entire doc
    var toObjectOptions = {};

    toObjectOptions.retainKeyOrder = this.schema.options.retainKeyOrder;
    toObjectOptions.depopulate = 1;
    toObjectOptions._skipDepopulateTopLevel = true;
    toObjectOptions.transform = false;
    toObjectOptions.flattenDecimals = false;

    var obj = this.toObject(toObjectOptions);

    if ((obj || {})._id === void 0) {
      // documents must have an _id else mongoose won't know
      // what to update later if more changes are made. the user
      // wouldn't know what _id was generated by mongodb either
      // nor would the ObjectId generated my mongodb necessarily
      // match the schema definition.
      setTimeout(function() {
        callback(new Error('document must have an _id before saving'));
      }, 0);
      return;
    }

    this.$__version(true, obj);
    this.collection.insert(obj, safe, function(err, ret) {
      if (err) {
        _this.isNew = true;
        _this.emit('isNew', true);
        _this.constructor.emit('isNew', true);

        callback(err);
        return;
      }

      callback(null, ret);
    });
    this.$__reset();
    this.isNew = false;
    this.emit('isNew', false);
    this.constructor.emit('isNew', false);
    // Make it possible to retry the insert
    this.$__.inserting = true;
  } else {
    // Make sure we don't treat it as a new object on error,
    // since it already exists
    this.$__.inserting = false;

    var delta = this.$__delta();

    if (delta) {
      if (delta instanceof Error) {
        callback(delta);
        return;
      }

      var where = this.$__where(delta[0]);
      if (where instanceof Error) {
        callback(where);
        return;
      }

      if (this.$where) {
        keys = Object.keys(this.$where);
        len = keys.length;
        for (i = 0; i < len; ++i) {
          where[keys[i]] = this.$where[keys[i]];
        }
      }

      this.collection.update(where, delta[1], safe, function(err, ret) {
        if (err) {
          callback(err);
          return;
        }
        ret.$where = where;
        callback(null, ret);
      });
    } else {
      this.$__reset();
      callback();
      return;
    }

    this.emit('isNew', false);
    this.constructor.emit('isNew', false);
  }
};
```
<!--endsec-->


## Model#collection

Collection the model uses.

<!--sec data-title="源码" data-id="Model_collection" data-show=true data-collapse=true ces-->
```js
Model.prototype.collection;
```
<!--endsec-->


## Model#db

Connection the model uses.

<!--sec data-title="源码" data-id="Model_db" data-show=true data-collapse=true ces-->
```js
Model.prototype.db;
```
<!--endsec-->


## Model#discriminators

Registered discriminators for this model.

<!--sec data-title="源码" data-id="Model_discriminators" data-show=true data-collapse=true ces-->
```js
Model.discriminators;
```
<!--endsec-->


## Model#modelName

The name of the model

<!--sec data-title="源码" data-id="Model_modelName" data-show=true data-collapse=true ces-->
```js
Model.prototype.modelName;
```
<!--endsec-->


## Model#schema

Schema the model uses.

<!--sec data-title="源码" data-id="Model_schema" data-show=true data-collapse=true ces-->
```js
Model.schema;
```
<!--endsec-->


-----

# schema/array.js

> 源码：[schema/array.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema/array.js)


## SchemaArray#checkRequired(value)


Check if the given value satisfies a required validator. The given value
must be not null nor undefined, and have a positive length.

##### 参数：

  * `value` &lt;[Any][]&gt;

##### 返回值：

  * &lt;[Boolean][]&gt;

<!--sec data-title="源码" data-id="SchemaArray_checkRequired" data-show=true data-collapse=true ces-->
```js
SchemaArray.prototype.checkRequired = function(value) {
  return !!(value && value.length);
};
```
<!--endsec-->


## SchemaArray(key, cast, options)

Array SchemaType constructor

##### 参数：

  * `key` &lt;[String][]&gt;

  * `cast` <SchemaType>

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [SchemaType]()

<!--sec data-title="源码" data-id="SchemaArray" data-show=true data-collapse=true ces-->
```js
function SchemaArray(key, cast, options, schemaOptions) {
  var typeKey = 'type';
  if (schemaOptions && schemaOptions.typeKey) {
    typeKey = schemaOptions.typeKey;
  }

  if (cast) {
    var castOptions = {};

    if (utils.getFunctionName(cast.constructor) === 'Object') {
      if (cast[typeKey]) {
        // support { type: Woot }
        castOptions = utils.clone(cast); // do not alter user arguments
        delete castOptions[typeKey];
        cast = cast[typeKey];
      } else {
        cast = Mixed;
      }
    }

    // support { type: 'String' }
    var name = typeof cast === 'string'
        ? cast
        : utils.getFunctionName(cast);

    var caster = name in Types
        ? Types[name]
        : cast;

    this.casterConstructor = caster;
    if (typeof caster === 'function' && !caster.$isArraySubdocument) {
      this.caster = new caster(null, castOptions);
    } else {
      this.caster = caster;
    }

    if (!(this.caster instanceof EmbeddedDoc)) {
      this.caster.path = key;
    }
  }

  this.$isMongooseArray = true;

  SchemaType.call(this, key, options, 'Array');

  var defaultArr;
  var fn;

  if (this.defaultValue != null) {
    defaultArr = this.defaultValue;
    fn = typeof defaultArr === 'function';
  }

  if (!('defaultValue' in this) || this.defaultValue !== void 0) {
    this.default(function() {
      var arr = [];
      if (fn) {
        arr = defaultArr();
      } else if (defaultArr != null) {
        arr = arr.concat(defaultArr);
      }
      // Leave it up to `cast()` to convert the array
      return arr;
    });
  }
}
```
<!--endsec-->

## SchemaArray.schemaName

This schema type's name, to defend against minifiers that mangle
function names.

<!--sec data-title="源码" data-id="SchemaArray_schemaName" data-show=true data-collapse=true ces-->
```js
SchemaArray.schemaName = 'Array';
```
<!--endsec-->

-----


# schema/boolean.js

> 源码：[schema/boolean.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema/boolean.js)

## SchemaBoolean#checkRequired(value)

Check if the given value satisfies a required validator. For a boolean
to satisfy a required validator, it must be strictly equal to true or to
false.

##### 参数：

  * `value` &lt;[Any][]&gt;

##### 返回值：

  * &lt;[Boolean][]&gt;

<!--sec data-title="源码" data-id="SchemaBoolean_checkRequired" data-show=true data-collapse=true ces-->
```js
SchemaBoolean.prototype.checkRequired = function(value) {
  return value === true || value === false;
};
```
<!--endsec-->


## SchemaBoolean(path, options)

Boolean SchemaType constructor.

##### 参数：

  * `path` &lt;[String][]&gt;

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [SchemaType]()

<!--sec data-title="源码" data-id="SchemaBoolean" data-show=true data-collapse=true ces-->
```js
function SchemaBoolean(path, options) {
  SchemaType.call(this, path, options, 'Boolean');
}
```
<!--endsec-->


## SchemaBoolean.schemaName

This schema type's name, to defend against minifiers that mangle
function names.

<!--sec data-title="源码" data-id="SchemaBoolean_schemaName" data-show=true data-collapse=true ces-->
```js
SchemaBoolean.schemaName = 'Boolean';
```
<!--endsec-->

----



# schema/mixed.js

> 源码：[schema/mixed.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema/mixed.js)


## Mixed(path, options)


Mixed SchemaType constructor.

##### 参数：

  * `path` &lt;[String][]&gt;

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [SchemaType]()

<!--sec data-title="源码" data-id="Mixed" data-show=true data-collapse=true ces-->
```js
function Mixed(path, options) {
  if (options && options.default) {
    var def = options.default;
    if (Array.isArray(def) && def.length === 0) {
      // make sure empty array defaults are handled
      options.default = Array;
    } else if (!options.shared && utils.isObject(def) && Object.keys(def).length === 0) {
      // prevent odd "shared" objects between documents
      options.default = function() {
        return {};
      };
    }
  }

  SchemaType.call(this, path, options, 'Mixed');
}
```
<!--endsec-->

## Mixed.schemaName

This schema type's name, to defend against minifiers that mangle
function names.

<!--sec data-title="源码" data-id="Mixed_schemaName" data-show=true data-collapse=true ces-->
```js
Mixed.schemaName = 'Mixed';
```
<!--endsec-->

------



# schema/embedded.js

> 源码：[schema/embedded.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema/embedded.js)


## Embedded#discriminator(name, schema)

Adds a discriminator to this property

##### 参数：

  * `name` &lt;[String][]&gt;

  * `schema` <Schema> fields to add to the schema for instances of this sub-class

<!--sec data-title="源码" data-id="Embedded_discriminator" data-show=true data-collapse=true ces-->
```js
Embedded.prototype.discriminator = function(name, schema) {
  discriminator(this.caster, name, schema);

  this.caster.discriminators[name] = _createConstructor(schema);

  return this.caster.discriminators[name];
};
```
<!--endsec-->


## Embedded(schema, key, options)

Sub-schema schematype constructor

##### 参数：

  * `schema` <Schema>

  * `key` &lt;[String][]&gt;

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [SchemaType]()

<!--sec data-title="源码" data-id="Embedded" data-show=true data-collapse=true ces-->
```js
function Embedded(schema, path, options) {
  this.caster = _createConstructor(schema);
  this.caster.prototype.$basePath = path;
  this.schema = schema;
  this.$isSingleNested = true;
  SchemaType.call(this, path, options, 'Embedded');
}
```
<!--endsec-->


------


# schema/buffer.js

> 源码：[schema/buffer.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema/buffer.js)

## SchemaBuffer#checkRequired(value, doc)

Check if the given value satisfies a required validator. To satisfy a
required validator, a buffer must not be null or undefined and have
non-zero length.

##### 参数：

  * `value` &lt;[Any][]&gt;

  * `doc` <Document>

##### 返回值：

&lt;[Boolean][]&gt;

<!--sec data-title="源码" data-id="SchemaBuffer_checkRequired" data-show=true data-collapse=true ces-->
```js
SchemaBuffer.prototype.checkRequired = function(value, doc) {
  if (SchemaType._isRef(this, value, doc, true)) {
    return !!value;
  }
  return !!(value && value.length);
};
```
<!--endsec-->


## SchemaBuffer(key, options)

Buffer SchemaType constructor

##### 参数：

  * `key` &lt;[String][]&gt;

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [SchemaType]()

<!--sec data-title="源码" data-id="SchemaBuffer" data-show=true data-collapse=true ces-->
```js
function SchemaBuffer(key, options) {
  SchemaType.call(this, key, options, 'Buffer');
}
```
<!--endsec-->


## SchemaBuffer#subtype(subtype)

Sets the default subtype
for this buffer. You can find a list of allowed subtypes here.

##### 参数：

  * `subtype` <Number> the default subtype

##### 返回值：

  * <SchemaType> this

##### 示例：

```js
var s = new Schema({ uuid: { type: Buffer, subtype: 4 }});
var M = db.model('M', s);
var m = new M({ uuid: 'test string' });
m.uuid._subtype; // 4
```

<!--sec data-title="源码" data-id="SchemaBuffer_subtype" data-show=true data-collapse=true ces-->
```js
SchemaBuffer.prototype.subtype = function(subtype) {
  this.options.subtype = subtype;
  return this;
};
```
<!--endsec-->



## SchemaBuffer.schemaName

This schema type's name, to defend against minifiers that mangle
function names.

<!--sec data-title="源码" data-id="SchemaBuffer_schemaName" data-show=true data-collapse=true ces-->
```js
SchemaBuffer.schemaName = 'Buffer';
```
<!--endsec-->

----


# schema/objectid.js

> 源码：[schema/objectid.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema/objectid.js)

## ObjectId#auto(turnOn)

Adds an auto-generated ObjectId default if turnOn is true.

##### 参数：

  * `turnOn` &lt;[Boolean][]&gt; auto generated ObjectId defaults

##### 返回值：

  * <SchemaType> this

<!--sec data-title="源码" data-id="ObjectId_auto" data-show=true data-collapse=true ces-->
```js
ObjectId.prototype.auto = function(turnOn) {
  if (turnOn) {
    this.default(defaultId);
    this.set(resetId);
  }

  return this;
};
```
<!--endsec-->


## ObjectId#checkRequired(value, doc)

Check if the given value satisfies a required validator.

##### 参数：

  * `value` &lt;[Any][]&gt;

  * `doc` <Document>

##### 返回值：

  * &lt;[Boolean][]&gt;

<!--sec data-title="源码" data-id="ObjectId_checkRequired" data-show=true data-collapse=true ces-->
```js
ObjectId.prototype.checkRequired = function checkRequired(value, doc) {
  if (SchemaType._isRef(this, value, doc, true)) {
    return !!value;
  }
  return value instanceof oid;
};
```
<!--endsec-->



## ObjectId(key, options)

ObjectId SchemaType constructor.

##### 参数：

  * `key` &lt;[String][]&gt;

  * `options` &lt;[Object][]&gt;

##### 继承：

  * SchemaType

<!--sec data-title="源码" data-id="ObjectId" data-show=true data-collapse=true ces-->
```js
function ObjectId(key, options) {
  var isKeyHexStr = typeof key === 'string' && key.length === 24 && /^a-f0-9$/i.test(key);
  var suppressWarning = options && options.suppressWarning;
  if ((isKeyHexStr || typeof key === 'undefined') && !suppressWarning) {
    console.warn('mongoose: To create a new ObjectId please try ' +
      '`Mongoose.Types.ObjectId` instead of using ' +
      '`Mongoose.Schema.ObjectId`. Set the `suppressWarning` option if ' +
      'you\'re trying to create a hex char path in your schema.');
    console.trace();
  }
  SchemaType.call(this, key, options, 'ObjectID');
}
```
<!--endsec-->


## ObjectId.schemaName

This schema type's name, to defend against minifiers that mangle
function names.

<!--sec data-title="源码" data-id="ObjectId_schemaName" data-show=true data-collapse=true ces-->
```js
ObjectId.schemaName = 'ObjectId';
```
<!--endsec-->


-----


# schema/string.js

> 源码：[schema/string.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema/string.js)


## SchemaString#checkRequired(value, doc)

Check if the given value satisfies the required validator. The value is
considered valid if it is a string (that is, not null or undefined) and
has positive length. The required validator will fail for empty
strings.

##### 参数：

  * `value` &lt;[Any][]&gt;

  * `doc` <Document>

##### 返回值：

  * &lt;[Boolean][]&gt;

<!--sec data-title="源码" data-id="SchemaString_checkRequired" data-show=true data-collapse=true ces-->
```js
SchemaString.prototype.checkRequired = function checkRequired(value, doc) {
  if (SchemaType._isRef(this, value, doc, true)) {
    return !!value;
  }
  return (value instanceof String || typeof value === 'string') && value.length;
};
```
<!--endsec-->


## SchemaString#enum([args...])

Adds an enum validator

##### 参数：

  * `[args...]` <String, Object> enumeration values

##### 返回值：

  * <SchemaType> this

##### 参见：

  * [Customized Error Messages]()

##### 示例：

```js
var states = ['opening', 'open', 'closing', 'closed']
var s = new Schema({ state: { type: String, enum: states }})
var M = db.model('M', s)
var m = new M({ state: 'invalid' })
m.save(function (err) {
  console.error(String(err)) // ValidationError: `invalid` is not a valid enum value for path `state`.
  m.state = 'open'
  m.save(callback) // success
})

// or with custom error messages
var enum = {
  values: ['opening', 'open', 'closing', 'closed'],
  message: 'enum validator failed for path `{PATH}` with value `{VALUE}`'
}
var s = new Schema({ state: { type: String, enum: enum }})
var M = db.model('M', s)
var m = new M({ state: 'invalid' })
m.save(function (err) {
  console.error(String(err)) // ValidationError: enum validator failed for path `state` with value `invalid`
  m.state = 'open'
  m.save(callback) // success
})
```

<!--sec data-title="源码" data-id="SchemaString_enum" data-show=true data-collapse=true ces-->
```js
SchemaString.prototype.enum = function() {
  if (this.enumValidator) {
    this.validators = this.validators.filter(function(v) {
      return v.validator !== this.enumValidator;
    }, this);
    this.enumValidator = false;
  }

  if (arguments[0] === void 0 || arguments[0] === false) {
    return this;
  }

  var values;
  var errorMessage;

  if (utils.isObject(arguments[0])) {
    values = arguments[0].values;
    errorMessage = arguments[0].message;
  } else {
    values = arguments;
    errorMessage = MongooseError.messages.String.enum;
  }

  for (var i = 0; i < values.length; i++) {
    if (undefined !== values[i]) {
      this.enumValues.push(this.cast(values[i]));
    }
  }

  var vals = this.enumValues;
  this.enumValidator = function(v) {
    return undefined === v || ~vals.indexOf(v);
  };
  this.validators.push({
    validator: this.enumValidator,
    message: errorMessage,
    type: 'enum',
    enumValues: vals
  });

  return this;
};
```

<!--endsec-->


## SchemaString#lowercase()


Adds a lowercase setter.

##### 返回值：

  * <SchemaType> this

##### 示例：

```js
var s = new Schema({ email: { type: String, lowercase: true }})
var M = db.model('M', s);
var m = new M({ email: 'SomeEmail@example.COM' });
console.log(m.email) // someemail@example.com
```

##### 注意：

Setters do not run on queries by default. Use the runSettersOnQuery option:

```js
 // Must use `runSettersOnQuery` as shown below, otherwise `email` will
 // **not** be lowercased.
 M.updateOne({}, { $set: { email: 'SomeEmail@example.COM' } }, { runSettersOnQuery: true });
```

<!--sec data-title="源码" data-id="SchemaString_lowercase" data-show=true data-collapse=true ces-->
```js
SchemaString.prototype.lowercase = function(shouldApply) {
  if (arguments.length > 0 && !shouldApply) {
    return this;
  }
  return this.set(function(v, self) {
    if (typeof v !== 'string') {
      v = self.cast(v);
    }
    if (v) {
      return v.toLowerCase();
    }
    return v;
  });
};
```
<!--endsec-->



## SchemaString#match(regExp, [message])

Sets a regexp validator.

##### 参数：

  * `regExp` <RegExp> regular expression to test against

  * `[message]` &lt;[String][]&gt; optional custom error message

##### 返回值：

  * <SchemaType> this

##### 参见：

  * [Customized Error Messages]()

Any value that does not pass regExp.test(val) will fail validation.

##### 示例：

```js
var s = new Schema({ name: { type: String, match: /^a/ }})
var M = db.model('M', s)
var m = new M({ name: 'I am invalid' })
m.validate(function (err) {
  console.error(String(err)) // "ValidationError: Path `name` is invalid (I am invalid)."
  m.name = 'apples'
  m.validate(function (err) {
    assert.ok(err) // success
  })
})

// using a custom error message
var match = [ /\.html$/, "That file doesn't end in .html ({VALUE})" ];
var s = new Schema({ file: { type: String, match: match }})
var M = db.model('M', s);
var m = new M({ file: 'invalid' });
m.validate(function (err) {
  console.log(String(err)) // "ValidationError: That file doesn't end in .html (invalid)"
})
```
Empty strings, undefined, and null values always pass the match validator. If you require these values, enable the required validator also.

```js
var s = new Schema({ name: { type: String, match: /^a/, required: true }})
```
<!--sec data-title="源码" data-id="SchemaString_match" data-show=true data-collapse=true ces-->
```js
SchemaString.prototype.match = function match(regExp, message) {
  // yes, we allow multiple match validators

  var msg = message || MongooseError.messages.String.match;

  var matchValidator = function(v) {
    if (!regExp) {
      return false;
    }

    var ret = ((v != null && v !== '')
        ? regExp.test(v)
        : true);
    return ret;
  };

  this.validators.push({
    validator: matchValidator,
    message: msg,
    type: 'regexp',
    regexp: regExp
  });
  return this;
};
```
<!--endsec-->

## SchemaString#maxlength(value, [message])

Sets a maximum length validator.

##### 参数：

    * `value` <Number> maximum string length

    * `[message]` &lt;[String][]&gt; optional custom error message

##### 返回值：

    * <SchemaType> this

##### 参见：

    * [Customized Error Messages]()

##### 示例：

```js
var schema = new Schema({ postalCode: { type: String, maxlength: 9 }})
var Address = db.model('Address', schema)
var address = new Address({ postalCode: '9512512345' })
address.save(function (err) {
  console.error(err) // validator error
  address.postalCode = '95125';
  address.save() // success
})

// custom error messages
// We can also use the special {MAXLENGTH} token which will be replaced with the maximum allowed length
var maxlength = [9, 'The value of path `{PATH}` (`{VALUE}`) exceeds the maximum allowed length ({MAXLENGTH}).'];
var schema = new Schema({ postalCode: { type: String, maxlength: maxlength }})
var Address = mongoose.model('Address', schema);
var address = new Address({ postalCode: '9512512345' });
address.validate(function (err) {
  console.log(String(err)) // ValidationError: The value of path `postalCode` (`9512512345`) exceeds the maximum allowed length (9).
})
```
<!--sec data-title="源码" data-id="SchemaString_maxlength" data-show=true data-collapse=true ces-->
```js
SchemaString.prototype.maxlength = function(value, message) {
  if (this.maxlengthValidator) {
    this.validators = this.validators.filter(function(v) {
      return v.validator !== this.maxlengthValidator;
    }, this);
  }

  if (value !== null && value !== undefined) {
    var msg = message || MongooseError.messages.String.maxlength;
    msg = msg.replace(/{MAXLENGTH}/, value);
    this.validators.push({
      validator: this.maxlengthValidator = function(v) {
        return v === null || v.length <= value;
      },
      message: msg,
      type: 'maxlength',
      maxlength: value
    });
  }

  return this;
};
```
<!--endsec-->



## SchemaString#minlength(value, [message])

Sets a minimum length validator.

##### 参数：

  * `value` <Number> minimum string length

  * `[message]` &lt;[String][]&gt; optional custom error message

##### 返回值：

  * <SchemaType> this

##### 参见：

  * [Customized Error Messages]()

##### 示例：

```js
var schema = new Schema({ postalCode: { type: String, minlength: 5 }})
var Address = db.model('Address', schema)
var address = new Address({ postalCode: '9512' })
address.save(function (err) {
  console.error(err) // validator error
  address.postalCode = '95125';
  address.save() // success
})

// custom error messages
// We can also use the special {MINLENGTH} token which will be replaced with the minimum allowed length
var minlength = [5, 'The value of path `{PATH}` (`{VALUE}`) is shorter than the minimum allowed length ({MINLENGTH}).'];
var schema = new Schema({ postalCode: { type: String, minlength: minlength }})
var Address = mongoose.model('Address', schema);
var address = new Address({ postalCode: '9512' });
address.validate(function (err) {
  console.log(String(err)) // ValidationError: The value of path `postalCode` (`9512`) is shorter than the minimum length (5).
})

```
<!--sec data-title="源码" data-id="SchemaString_minlength" data-show=true data-collapse=true ces-->
```js
SchemaString.prototype.minlength = function(value, message) {
  if (this.minlengthValidator) {
    this.validators = this.validators.filter(function(v) {
      return v.validator !== this.minlengthValidator;
    }, this);
  }

  if (value !== null && value !== undefined) {
    var msg = message || MongooseError.messages.String.minlength;
    msg = msg.replace(/{MINLENGTH}/, value);
    this.validators.push({
      validator: this.minlengthValidator = function(v) {
        return v === null || v.length >= value;
      },
      message: msg,
      type: 'minlength',
      minlength: value
    });
  }

  return this;
};
```
<!--endsec-->


## SchemaString(key, options)

String SchemaType constructor.

##### 参数：

  * `key` &lt;[String][]&gt;

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [SchemaType]()

<!--sec data-title="源码" data-id="SchemaString" data-show=true data-collapse=true ces-->
```js
function SchemaString(key, options) {
  this.enumValues = [];
  this.regExp = null;
  SchemaType.call(this, key, options, 'String');
}
```
<!--endsec-->


## SchemaString#trim()

Adds a trim setter.

##### 返回值：

  * <SchemaType> this

The string value will be trimmed when set.

##### 示例：

```js
var s = new Schema({ name: { type: String, trim: true }})
var M = db.model('M', s)
var string = ' some name '
console.log(string.length) // 11
var m = new M({ name: string })
console.log(m.name.length) // 9
```

##### 注意：

Setters do not run on queries by default. Use the runSettersOnQuery option:

```js
 // Must use `runSettersOnQuery` as shown below, otherwise `email` will
 // **not** be lowercased.
 M.updateOne({}, { $set: { email: 'SomeEmail@example.COM' } }, { runSettersOnQuery: true });
```

<!--sec data-title="源码" data-id="SchemaString_trim" data-show=true data-collapse=true ces-->
```js
SchemaString.prototype.trim = function(shouldTrim) {
  if (arguments.length > 0 && !shouldTrim) {
    return this;
  }
  return this.set(function(v, self) {
    if (typeof v !== 'string') {
      v = self.cast(v);
    }
    if (v) {
      return v.trim();
    }
    return v;
  });
};
```
<!--endsec-->



## SchemaString#uppercase()

Adds an uppercase setter.

##### 返回值：

  * <SchemaType> this

##### 示例：

```js
var s = new Schema({ caps: { type: String, uppercase: true }})
var M = db.model('M', s);
var m = new M({ caps: 'an example' });
console.log(m.caps) // AN EXAMPLE
```

##### 注意：

Setters do not run on queries by default. Use the runSettersOnQuery option:

```js
 // Must use `runSettersOnQuery` as shown below, otherwise `email` will
 // **not** be lowercased.
 M.updateOne({}, { $set: { email: 'SomeEmail@example.COM' } }, { runSettersOnQuery: true });
```

<!--sec data-title="源码" data-id="SchemaString_uppercase" data-show=true data-collapse=true ces-->
```js
SchemaString.prototype.uppercase = function(shouldApply) {
  if (arguments.length > 0 && !shouldApply) {
    return this;
  }
  return this.set(function(v, self) {
    if (typeof v !== 'string') {
      v = self.cast(v);
    }
    if (v) {
      return v.toUpperCase();
    }
    return v;
  });
};
```
<!--endsec-->


## SchemaString.schemaName

This schema type's name, to defend against minifiers that mangle
function names.

<!--sec data-title="源码" data-id="SchemaString_schemaName" data-show=true data-collapse=true ces-->
```js
SchemaString.schemaName = 'String';
```
<!--endsec-->

-----


# schema/decimal128.js

> 源码：[schema/decimal128.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema/decimal128.js)


## Decimal128#checkRequired(value, doc)

Check if the given value satisfies a required validator.

##### 参数：

  * `value` &lt;[Any][]&gt;

  * `doc` <Document>

##### 返回值：

  * &lt;[Boolean][]&gt;

<!--sec data-title="源码" data-id="Decimal128_checkRequired" data-show=true data-collapse=true ces-->
```js
Decimal128.prototype.checkRequired = function checkRequired(value, doc) {
  if (SchemaType._isRef(this, value, doc, true)) {
    return !!value;
  }
  return value instanceof Decimal128Type;
};
```
<!--endsec-->


## Decimal128(key, options)

Decimal128 SchemaType constructor.

##### 参数：

  * `key` &lt;[String][]&gt;

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [SchemaType]()

<!--sec data-title="源码" data-id="Decimal128" data-show=true data-collapse=true ces-->
```js
function Decimal128(key, options) {
  SchemaType.call(this, key, options, 'Decimal128');
}
```
<!--endsec-->


## Decimal128.schemaName

This schema type's name, to defend against minifiers that mangle
function names.

<!--sec data-title="源码" data-id="Decimal128_schemaName" data-show=true data-collapse=true ces-->
```js
Decimal128.schemaName = 'Decimal128';
```
<!--endsec-->

-----


# schema/documentarray.js

## DocumentArray(key, schema, options)

SubdocsArray SchemaType constructor

##### 参数：

  * `key` &lt;[String][]&gt;

  * `schema` <Schema>

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [SchemaArray]()

<!--sec data-title="源码" data-id="DocumentArray" data-show=true data-collapse=true ces-->
```js
function DocumentArray(key, schema, options) {
  var EmbeddedDocument = _createConstructor(schema, options);
  EmbeddedDocument.prototype.$basePath = key;

  ArrayType.call(this, key, EmbeddedDocument, options);

  this.schema = schema;
  this.$isMongooseDocumentArray = true;
  var fn = this.defaultValue;

  if (!('defaultValue' in this) || fn !== void 0) {
    this.default(function() {
      var arr = fn.call(this);
      if (!Array.isArray(arr)) {
        arr = [arr];
      }
      // Leave it up to `cast()` to convert this to a documentarray
      return arr;
    });
  }
}
```
<!--endsec-->


## DocumentArray.schemaName

This schema type's name, to defend against minifiers that mangle
function names.

<!--sec data-title="源码" data-id="DocumentArray_schemaName" data-show=true data-collapse=true ces-->
```js
DocumentArray.schemaName = 'DocumentArray';
```
<!--endsec-->


# schema/date.js

> 源码：[schema/date.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema/date.js)

## SchemaDate#checkRequired(value, doc)

Check if the given value satisfies a required validator. To satisfy
a required validator, the given value must be an instance of Date.

##### 参数：

  * `value` &lt;[Any][]&gt;

  * `doc` <Document>

##### 返回值：

  * &lt;[Boolean][]&gt;

<!--sec data-title="源码" data-id="SchemaDate_checkRequired" data-show=true data-collapse=true ces-->
```js
SchemaDate.prototype.checkRequired = function(value) {
  return value instanceof Date;
};
```
<!--endsec-->


## SchemaDate#expires(when)

Declares a TTL index (rounded to the nearest second) for Date types only.

##### 参数：

  * `when` <Number, String>

##### 返回值：

  * <SchemaType> this

This sets the expireAfterSeconds index option available in MongoDB >= 2.1.2.
This index type is only compatible with Date types.

##### 示例：

```js
// expire in 24 hours
new Schema({ createdAt: { type: Date, expires: 60*60*24 }});
expires utilizes the ms module from guille allowing us to use a friendlier syntax:
```
##### 示例：

```js
// expire in 24 hours
new Schema({ createdAt: { type: Date, expires: '24h' }});

// expire in 1.5 hours
new Schema({ createdAt: { type: Date, expires: '1.5h' }});

// expire in 7 days
var schema = new Schema({ createdAt: Date });
schema.path('createdAt').expires('7d');
```
<!--sec data-title="源码" data-id="SchemaDate_expires" data-show=true data-collapse=true ces-->
```js
SchemaDate.prototype.expires = function(when) {
  if (!this._index || this._index.constructor.name !== 'Object') {
    this._index = {};
  }

  this._index.expires = when;
  utils.expires(this._index);
  return this;
};
```
<!--endsec-->


## SchemaDate#max(maximum, [message])

Sets a maximum date validator.

##### 参数：

  * `maximum` <Date> date

  * `[message]` &lt;[String][]&gt; optional custom error message

##### 返回值：

  * <SchemaType> this

##### 参见：

  * [Customized Error Messages]()

##### 示例：

```js
var s = new Schema({ d: { type: Date, max: Date('2014-01-01') }})
var M = db.model('M', s)
var m = new M({ d: Date('2014-12-08') })
m.save(function (err) {
  console.error(err) // validator error
  m.d = Date('2013-12-31');
  m.save() // success
})

// custom error messages
// We can also use the special {MAX} token which will be replaced with the invalid value
var max = [Date('2014-01-01'), 'The value of path `{PATH}` ({VALUE}) exceeds the limit ({MAX}).'];
var schema = new Schema({ d: { type: Date, max: max }})
var M = mongoose.model('M', schema);
var s= new M({ d: Date('2014-12-08') });
s.validate(function (err) {
  console.log(String(err)) // ValidationError: The value of path `d` (2014-12-08) exceeds the limit (2014-01-01).
})
```
<!--sec data-title="源码" data-id="SchemaDate_max" data-show=true data-collapse=true ces-->
```js
SchemaDate.prototype.max = function(value, message) {
  if (this.maxValidator) {
    this.validators = this.validators.filter(function(v) {
      return v.validator !== this.maxValidator;
    }, this);
  }

  if (value) {
    var msg = message || MongooseError.messages.Date.max;
    msg = msg.replace(/{MAX}/, (value === Date.now ? 'Date.now()' : this.cast(value).toString()));
    var _this = this;
    this.validators.push({
      validator: this.maxValidator = function(val) {
        var max = (value === Date.now ? value() : _this.cast(value));
        return val === null || val.valueOf() <= max.valueOf();
      },
      message: msg,
      type: 'max',
      max: value
    });
  }

  return this;
};

```
<!--endsec-->

## SchemaDate#min(value, [message])

Sets a minimum date validator.

##### 参数：

  * `value` <Date> minimum date

  * `[message]` &lt;[String][]&gt; optional custom error message

##### 返回值：

  * <SchemaType> this

##### 参见：

  * [Customized Error Messages]()

##### 示例：

```js
var s = new Schema({ d: { type: Date, min: Date('1970-01-01') }})
var M = db.model('M', s)
var m = new M({ d: Date('1969-12-31') })
m.save(function (err) {
  console.error(err) // validator error
  m.d = Date('2014-12-08');
  m.save() // success
})

// custom error messages
// We can also use the special {MIN} token which will be replaced with the invalid value
var min = [Date('1970-01-01'), 'The value of path `{PATH}` ({VALUE}) is beneath the limit ({MIN}).'];
var schema = new Schema({ d: { type: Date, min: min }})
var M = mongoose.model('M', schema);
var s= new M({ d: Date('1969-12-31') });
s.validate(function (err) {
  console.log(String(err)) // ValidationError: The value of path `d` (1969-12-31) is before the limit (1970-01-01).
})
```
<!--sec data-title="源码" data-id="SchemaDate_min" data-show=true data-collapse=true ces-->
```js
SchemaDate.prototype.min = function(value, message) {
  if (this.minValidator) {
    this.validators = this.validators.filter(function(v) {
      return v.validator !== this.minValidator;
    }, this);
  }

  if (value) {
    var msg = message || MongooseError.messages.Date.min;
    msg = msg.replace(/{MIN}/, (value === Date.now ? 'Date.now()' : this.cast(value).toString()));
    var _this = this;
    this.validators.push({
      validator: this.minValidator = function(val) {
        var min = (value === Date.now ? value() : _this.cast(value));
        return val === null || val.valueOf() >= min.valueOf();
      },
      message: msg,
      type: 'min',
      min: value
    });
  }

  return this;
};

```
<!--endsec-->

## SchemaDate(key, options)

Date SchemaType constructor.

##### 参数：

  * `key` &lt;[String][]&gt;

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [SchemaType]()

<!--sec data-title="源码" data-id="SchemaDate" data-show=true data-collapse=true ces-->
```js
function SchemaDate(key, options) {
  SchemaType.call(this, key, options, 'Date');
}
```
<!--endsec-->


## SchemaDate.schemaName

This schema type's name, to defend against minifiers that mangle
function names.

<!--sec data-title="源码" data-id="SchemaDate_schemaName" data-show=true data-collapse=true ces-->
```js
SchemaDate.schemaName = 'Date';
```
<!--endsec-->

------


# schema/number.js

> 源码：[schema/number.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schema/number.js)


## SchemaNumber#checkRequired(value, doc)

Check if the given value satisfies a required validator.

##### 参数：

  * `value` &lt;[Any][]&gt;

  * `doc` <Document>

##### 返回值：

  * &lt;[Boolean][]&gt;

<!--sec data-title="源码" data-id="SchemaNumber_checkRequired" data-show=true data-collapse=true ces-->
```js
SchemaNumber.prototype.checkRequired = function checkRequired(value, doc) {
  if (SchemaType._isRef(this, value, doc, true)) {
    return !!value;
  }
  return typeof value === 'number' || value instanceof Number;
};
```
<!--endsec-->


## SchemaNumber#max(maximum, [message])

Sets a maximum number validator.

##### 参数：

  * `maximum` <Number> number

  * `[message]` &lt;[String][]&gt; optional custom error message

##### 返回值：

  * <SchemaType> this

##### 参见：

  * [Customized Error Messages]()

##### 示例：

```js
var s = new Schema({ n: { type: Number, max: 10 }})
var M = db.model('M', s)
var m = new M({ n: 11 })
m.save(function (err) {
  console.error(err) // validator error
  m.n = 10;
  m.save() // success
})

// custom error messages
// We can also use the special {MAX} token which will be replaced with the invalid value
var max = [10, 'The value of path `{PATH}` ({VALUE}) exceeds the limit ({MAX}).'];
var schema = new Schema({ n: { type: Number, max: max }})
var M = mongoose.model('Measurement', schema);
var s= new M({ n: 4 });
s.validate(function (err) {
  console.log(String(err)) // ValidationError: The value of path `n` (4) exceeds the limit (10).
})
```
<!--sec data-title="源码" data-id="SchemaNumber_max" data-show=true data-collapse=true ces-->
```js
SchemaNumber.prototype.max = function(value, message) {
  if (this.maxValidator) {
    this.validators = this.validators.filter(function(v) {
      return v.validator !== this.maxValidator;
    }, this);
  }

  if (value !== null && value !== undefined) {
    var msg = message || MongooseError.messages.Number.max;
    msg = msg.replace(/{MAX}/, value);
    this.validators.push({
      validator: this.maxValidator = function(v) {
        return v == null || v <= value;
      },
      message: msg,
      type: 'max',
      max: value
    });
  }

  return this;
};
```
<!--endsec-->



## SchemaNumber#min(value, [message])

Sets a minimum number validator.

##### 参数：

  * `value` <Number> minimum number

  * `[message]` &lt;[String][]&gt; optional custom error message

##### 返回值：

  * <SchemaType> this

##### 参见：

  * [Customized Error Messages]()

##### 示例：

```js
var s = new Schema({ n: { type: Number, min: 10 }})
var M = db.model('M', s)
var m = new M({ n: 9 })
m.save(function (err) {
  console.error(err) // validator error
  m.n = 10;
  m.save() // success
})

// custom error messages
// We can also use the special {MIN} token which will be replaced with the invalid value
var min = [10, 'The value of path `{PATH}` ({VALUE}) is beneath the limit ({MIN}).'];
var schema = new Schema({ n: { type: Number, min: min }})
var M = mongoose.model('Measurement', schema);
var s= new M({ n: 4 });
s.validate(function (err) {
  console.log(String(err)) // ValidationError: The value of path `n` (4) is beneath the limit (10).
})
```

<!--sec data-title="源码" data-id="SchemaNumber_min" data-show=true data-collapse=true ces-->
```js
SchemaNumber.prototype.min = function(value, message) {
  if (this.minValidator) {
    this.validators = this.validators.filter(function(v) {
      return v.validator !== this.minValidator;
    }, this);
  }

  if (value !== null && value !== undefined) {
    var msg = message || MongooseError.messages.Number.min;
    msg = msg.replace(/{MIN}/, value);
    this.validators.push({
      validator: this.minValidator = function(v) {
        return v == null || v >= value;
      },
      message: msg,
      type: 'min',
      min: value
    });
  }

  return this;
};
```
<!--endsec-->


## SchemaNumber(key, options)

Number SchemaType constructor.

##### 参数：

  * `key` &lt;[String][]&gt;

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [SchemaType]()

<!--sec data-title="源码" data-id="SchemaNumber" data-show=true data-collapse=true ces-->
```js
function SchemaNumber(key, options) {
  SchemaType.call(this, key, options, 'Number');
}
```
<!--endsec-->


## SchemaNumber.schemaName

This schema type's name, to defend against minifiers that mangle
function names.

<!--sec data-title="源码" data-id="SchemaNumber_schemaName" data-show=true data-collapse=true ces-->
```js
SchemaNumber.schemaName = 'Number';
```
<!--endsec-->


------


# cursor/QueryCursor.js

> 源码：[cursor/QueryCursor.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/cursor/QueryCursor.js)


## QueryCursor#addCursorFlag(flag, value)

Adds a cursor flag.
Useful for setting the noCursorTimeout and tailable flags.

##### 参数：

  * `flag` &lt;[String][]&gt;

  * `value` &lt;[Boolean][]&gt;

##### 返回值：

  * <AggregationCursor> this

## QueryCursor#close(callback)

Marks this cursor as closed. Will stop streaming and subsequent calls to
next() will error.

##### 参数：

  * `callback` &lt;[Function][]&gt;

##### 返回值：

  * <Promise>

##### 参见：

  * [MongoDB](http://mongoosejs.com/docs/driver%20cursor#close http://mongodb.github.io/node-mongodb-native/2.1/api/Cursor.html#close)

## QueryCursor#eachAsync(fn, [options], [options.parallel], [callback])

Execute fn for every document in the cursor. If fn returns a promise,
will wait for the promise to resolve before iterating on to the next one.
Returns a promise that resolves when done.

##### 参数：

  * `fn` &lt;[Function][]&gt;

  * `[options]` &lt;[Object][]&gt;

  * `[options.parallel]` <Number> the number of promises to execute in parallel. Defaults to 1.

  * `[callback]` &lt;[Function][]&gt; executed when all docs have been processed

##### 返回值：

  * <Promise>



## QueryCursor#map(fn)

Registers a transform function which subsequently maps documents retrieved
via the streams interface or .next()

##### 参数：

  * `fn` &lt;[Function][]&gt;

##### 返回值：

  * <QueryCursor>

##### 示例：

```js
// Map documents returned by `data` events
Thing.
  find({ name: /^hello/ }).
  cursor().
  map(function (doc) {
   doc.foo = "bar";
   return doc;
  })
  on('data', function(doc) { console.log(doc.foo); });

// Or map documents returned by `.next()`
var cursor = Thing.find({ name: /^hello/ }).
  cursor().
  map(function (doc) {
    doc.foo = "bar";
    return doc;
  });
cursor.next(function(error, doc) {
  console.log(doc.foo);
});
```



## QueryCursor#next(callback)


Get the next document from this cursor. Will return null when there are
no documents left.

##### 参数：

  * callback &lt;[Function][]&gt;

##### 返回值：

  * <Promise>


## QueryCursor(query, options)

A QueryCursor is a concurrency primitive for processing query results
one document at a time. A QueryCursor fulfills the Node.js streams3 API,
in addition to several other mechanisms for loading documents from MongoDB
one at a time.

##### 参数：

  * `query` <Query>

  * `options` &lt;[Object][]&gt; query options passed to .find()

##### 继承：

  * [Readable](http://mongoosejs.com/docs/api.html#Readable)

##### 事件：

`cursor`: Emitted when the cursor is created

`error`: Emitted when an error occurred

`data`: Emitted when the stream is flowing and the next doc is ready

`end`: Emitted when the stream is exhausted

QueryCursors execute the model's pre find hooks, but not the model's
post find hooks.

Unless you're an advanced user, do not instantiate this class directly.
Use [Query#cursor()]() instead.

<!--sec data-title="源码" data-id="QueryCursor" data-show=true data-collapse=true ces-->
```js
function QueryCursor(query, options) {
  Readable.call(this, { objectMode: true });

  this.cursor = null;
  this.query = query;
  this._transforms = options.transform ? [options.transform] : [];
  var _this = this;
  var model = query.model;
  model.hooks.execPre('find', query, function() {
    model.collection.find(query._conditions, options, function(err, cursor) {
      if (_this._error) {
        cursor.close(function() {});
        _this.listeners('error').length > 0 && _this.emit('error', _this._error);
      }
      if (err) {
        return _this.emit('error', err);
      }
      _this.cursor = cursor;
      _this.emit('cursor', cursor);
    });
  });
}

util.inherits(QueryCursor, Readable);
```
<!--endsec-->


# cursor/AggregationCursor.js

> 源码：[cursor/AggregationCursor.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/cursor/AggregationCursor.js)


## AggregationCursor#addCursorFlag(flag, value)

Adds a cursor flag.
Useful for setting the noCursorTimeout and tailable flags.

##### 参数：

  * `flag` &lt;[String][]&gt;

  * `value` &lt;[Boolean][]&gt;

##### 返回值：

  * <AggregationCursor> this


## AggregationCursor(agg, options)

An AggregationCursor is a concurrency primitive for processing aggregation
results one document at a time. It is analogous to QueryCursor.

##### 参数：

  * `agg` <Aggregate>

  * `options` &lt;[Object][]&gt;

##### 继承：

  * [Readable](http://mongoosejs.com/docs/api.html#Readable)

##### 事件：

`cursor`: Emitted when the cursor is created

`error`: Emitted when an error occurred

`data`: Emitted when the stream is flowing and the next doc is ready

`end`: Emitted when the stream is exhausted

An AggregationCursor fulfills the [Node.js streams3 API](https://strongloop.com/strongblog/whats-new-io-js-beta-streams3/),
in addition to several other mechanisms for loading documents from MongoDB
one at a time.

Creating an AggregationCursor executes the model's pre aggregate hooks,
but not the model's post aggregate hooks.

Unless you're an advanced user, do not instantiate this class directly.
Use [Aggregate#cursor()](http://mongoosejs.com/docs/api.html#aggregate_Aggregate-cursor) instead.

<!--sec data-title="源码" data-id="AggregationCursor" data-show=true data-collapse=true ces-->
```js
function AggregationCursor(agg) {
  Readable.call(this, { objectMode: true });

  this.cursor = null;
  this.agg = agg;
  this._transforms = [];
  var model = agg._model;
  delete agg.options.cursor.useMongooseAggCursor;

  _init(model, this, agg);
}

util.inherits(AggregationCursor, Readable);
```
<!--endsec-->


## AggregationCursor#close(callback)

Marks this cursor as closed. Will stop streaming and subsequent calls to
next() will error.

##### 参数：

  * `callback` &lt;[Function][]&gt;

##### 返回值：

  * <Promise>

##### 参见：

  * [MongoDB](http://mongoosejs.com/docs/driver%20cursor#close http://mongodb.github.io/node-mongodb-native/2.1/api/Cursor.html#close)

## AggregationCursor#eachAsync(fn, [callback])

Execute fn for every document in the cursor. If fn returns a promise,
will wait for the promise to resolve before iterating on to the next one.
Returns a promise that resolves when done.

##### 参数：

  * `fn` &lt;[Function][]&gt;

  * `[callback]` &lt;[Function][]&gt; executed when all docs have been processed

##### 返回值：

  * <Promise>



## AggregationCursor#map(fn)

Registers a transform function which subsequently maps documents retrieved
via the streams interface or .next()

##### 参数：

  * `fn` &lt;[Function][]&gt;

##### 返回值：

  * <QueryCursor>

##### 示例：

```js
// Map documents returned by `data` events
Thing.
  find({ name: /^hello/ }).
  cursor().
  map(function (doc) {
   doc.foo = "bar";
   return doc;
  })
  on('data', function(doc) { console.log(doc.foo); });

// Or map documents returned by `.next()`
var cursor = Thing.find({ name: /^hello/ }).
  cursor().
  map(function (doc) {
    doc.foo = "bar";
    return doc;
  });
cursor.next(function(error, doc) {
  console.log(doc.foo);
});
```



## AggregationCursor#next(callback)

Get the next document from this cursor. Will return null when there are
no documents left.

##### 参数：

  * `callback` &lt;[Function][]&gt;

##### 返回值：

  * <Promise>



------



# schematype.js

> 源码：[schematype.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/schematype.js)


## SchemaType#default(val)

Sets a default value for this SchemaType.

##### 参数：

  * `val` <Function, T> the default value

##### 返回值：

  * <defaultValue>

##### 示例：

```js
var schema = new Schema({ n: { type: Number, default: 10 }})
var M = db.model('M', schema)
var m = new M;
console.log(m.n) // 10
```

Defaults can be either functions which return the value to use as the default or the literal value itself. Either way, the value will be cast based on its schema type before being set during document creation.

##### 示例：

```js
// values are cast:
var schema = new Schema({ aNumber: { type: Number, default: 4.815162342 }})
var M = db.model('M', schema)
var m = new M;
console.log(m.aNumber) // 4.815162342

// default unique objects for Mixed types:
var schema = new Schema({ mixed: Schema.Types.Mixed });
schema.path('mixed').default(function () {
  return {};
});

// if we don't use a function to return object literals for Mixed defaults,
// each document will receive a reference to the same object literal creating
// a "shared" object instance:
var schema = new Schema({ mixed: Schema.Types.Mixed });
schema.path('mixed').default({});
var M = db.model('M', schema);
var m1 = new M;
m1.mixed.added = 1;
console.log(m1.mixed); // { added: 1 }
var m2 = new M;
console.log(m2.mixed); // { added: 1 }
```

<!--sec data-title="源码" data-id="SchemaType_default" data-show=true data-collapse=true ces-->
```js
SchemaType.prototype.default = function(val) {
  if (arguments.length === 1) {
    if (val === void 0) {
      this.defaultValue = void 0;
      return void 0;
    }
    this.defaultValue = val;
    return this.defaultValue;
  } else if (arguments.length > 1) {
    this.defaultValue = utils.args(arguments);
  }
  return this.defaultValue;
};
```
<!--endsec-->

## SchemaType#get(fn)

Adds a getter to this schematype.

##### 参数：

  * `fn` &lt;[Function][]&gt;

##### 返回值：

  * <SchemaType> this

##### 示例：

```js
function dob (val) {
  if (!val) return val;
  return (val.getMonth() + 1) + "/" + val.getDate() + "/" + val.getFullYear();
}

// defining within the schema
var s = new Schema({ born: { type: Date, get: dob }})

// or by retreiving its SchemaType
var s = new Schema({ born: Date })
s.path('born').get(dob)
```
Getters allow you to transform the representation of the data as it travels from the raw mongodb document to the value that you see.

Suppose you are storing credit card numbers and you want to hide everything except the last 4 digits to the mongoose user. You can do so by defining a getter in the following way:

```js
function obfuscate (cc) {
  return '****-****-****-' + cc.slice(cc.length-4, cc.length);
}

var AccountSchema = new Schema({
  creditCardNumber: { type: String, get: obfuscate }
});

var Account = db.model('Account', AccountSchema);

Account.findById(id, function (err, found) {
  console.log(found.creditCardNumber); // '****-****-****-1234'
});
```

Getters are also passed a second argument, the schematype on which the getter was defined. This allows for tailored behavior based on options passed in the schema.

```js
function inspector (val, schematype) {
  if (schematype.options.required) {
    return schematype.path + ' is required';
  } else {
    return schematype.path + ' is not';
  }
}

var VirusSchema = new Schema({
  name: { type: String, required: true, get: inspector },
  taxonomy: { type: String, get: inspector }
})

var Virus = db.model('Virus', VirusSchema);

Virus.findById(id, function (err, virus) {
  console.log(virus.name);     // name is required
  console.log(virus.taxonomy); // taxonomy is not
})
```
<!--sec data-title="源码" data-id="SchemaType_get" data-show=true data-collapse=true ces-->
```js
SchemaType.prototype.get = function(fn) {
  if (typeof fn !== 'function') {
    throw new TypeError('A getter must be a function.');
  }
  this.getters.push(fn);
  return this;
};
```
<!--endsec-->


## SchemaType#index(options)

Declares the index options for this schematype.

##### 参数：

  * `options` <Object, Boolean, String>

##### 返回值：

  * <SchemaType> this

##### 示例：

```js
var s = new Schema({ name: { type: String, index: true }})
var s = new Schema({ loc: { type: [Number], index: 'hashed' }})
var s = new Schema({ loc: { type: [Number], index: '2d', sparse: true }})
var s = new Schema({ loc: { type: [Number], index: { type: '2dsphere', sparse: true }}})
var s = new Schema({ date: { type: Date, index: { unique: true, expires: '1d' }}})
Schema.path('my.path').index(true);
Schema.path('my.date').index({ expires: 60 });
Schema.path('my.path').index({ unique: true, sparse: true });
```

##### 注意：

Indexes are created in the background by default. Specify background: false to override.

[Direction doesn't matter for single key indexes](http://www.mongodb.org/display/DOCS/Indexes#Indexes-CompoundKeysIndexes)

<!--sec data-title="源码" data-id="SchemaType_index" data-show=true data-collapse=true ces-->
```js
SchemaType.prototype.index = function(options) {
  this._index = options;
  utils.expires(this._index);
  return this;
};
```
<!--endsec-->


## SchemaType#required(required, [options.isRequired], [options.ErrorConstructor], [message])


Adds a required validator to this SchemaType. The validator gets added
to the front of this SchemaType's validators array using unshift().

##### 参数：

  * `required` <Boolean, Function, Object> enable/disable the validator, or function that returns required boolean, or options object

  * `[options.isRequired]` <Boolean, Function> enable/disable the validator, or function that returns required boolean

  * `[options.ErrorConstructor]` &lt;[Function][]&gt; custom error constructor. The constructor receives 1 parameter, an object containing the validator properties.

  * `[message]` &lt;[String][]&gt; optional custom error message

##### 返回值：

  * <SchemaType> this

##### 参见：

  * [Customized Error Messages]()

  * [SchemaArray#checkRequired]()

  * [SchemaBoolean#checkRequired]()

  * [SchemaBuffer#checkRequired]()

  * [SchemaNumber#checkRequired]()

  * [SchemaObjectId#checkRequired]()

  * [SchemaString#checkRequired]()

##### 示例：

```js
var s = new Schema({ born: { type: Date, required: true }})

// or with custom error message

var s = new Schema({ born: { type: Date, required: '{PATH} is required!' }})

// or with a function

var s = new Schema({
  userId: ObjectId,
  username: {
    type: String,
    required: function() { return this.userId != null; }
  }
})

// or with a function and a custom message
var s = new Schema({
  userId: ObjectId,
  username: {
    type: String,
    required: [
      function() { return this.userId != null; },
      'username is required if id is specified'
    ]
  }
})

// or through the path API

Schema.path('name').required(true);

// with custom error messaging

Schema.path('name').required(true, 'grrr :( ');

// or make a path conditionally required based on a function
var isOver18 = function() { return this.age &gt;= 18; };
Schema.path('voterRegistrationId').required(isOver18);

```
The required validator uses the SchemaType's checkRequired function to
determine whether a given value satisfies the required validator. By default,
a value satisfies the required validator if val != null (that is, if
the value is not null nor undefined). However, most built-in mongoose schema
types override the default checkRequired function:

<!--sec data-title="源码" data-id="SchemaType_required" data-show=true data-collapse=true ces-->
```js
SchemaType.prototype.required = function(required, message) {
  var customOptions = {};
  if (typeof required === 'object') {
    customOptions = required;
    message = customOptions.message || message;
    required = required.isRequired;
  }

  if (required === false) {
    this.validators = this.validators.filter(function(v) {
      return v.validator !== this.requiredValidator;
    }, this);

    this.isRequired = false;
    return this;
  }

  var _this = this;
  this.isRequired = true;

  this.requiredValidator = function(v) {
    // in here, `this` refers to the validating document.
    // no validation when this path wasn't selected in the query.
    if ('isSelected' in this && !this.isSelected(_this.path) && !this.isModified(_this.path)) {
      return true;
    }

    return ((typeof required === 'function') && !required.apply(this)) ||
        _this.checkRequired(v, this);
  };
  this.originalRequiredValue = required;

  if (typeof required === 'string') {
    message = required;
    required = undefined;
  }

  var msg = message || MongooseError.messages.general.required;
  this.validators.unshift(utils.assign({}, customOptions, {
    validator: this.requiredValidator,
    message: msg,
    type: 'required'
  }));

  return this;
};

```
<!--endsec-->


## SchemaType(path, [options], [instance])

SchemaType constructor

##### 参数：

  * `path` &lt;[String][]&gt;

  * `[options]` &lt;[Object][]&gt;

  * `[instance]` &lt;[String][]&gt;

<!--sec data-title="源码" data-id="11" data-show=true data-collapse=true ces-->
```js
function SchemaType(path, options, instance) {
  this.path = path;
  this.instance = instance;
  this.validators = [];
  this.setters = [];
  this.getters = [];
  this.options = options;
  this._index = null;
  this.selected;

  for (var prop in options) {
    if (this[prop] && typeof this[prop] === 'function') {
      // { unique: true, index: true }
      if (prop === 'index' && this._index) {
        continue;
      }

      var val = options[prop];
      // Special case so we don't screw up array defaults, see gh-5780
      if (prop === 'default') {
        this.default(val);
        continue;
      }

      var opts = Array.isArray(val) ? val : [val];

      this[prop].apply(this, opts);
    }
  }

  Object.defineProperty(this, '$$context', {
    enumerable: false,
    configurable: false,
    writable: true,
    value: null
  });
}
```
<!--endsec-->


## SchemaType#select(val)

Sets default select() behavior for this path.

##### 参数：

  * `val` &lt;[Boolean][]&gt;

##### 返回值：

  * <SchemaType> this

Set to true if this path should always be included in the results, false if it should be excluded by default. This setting can be overridden at the query level.

##### 示例：

```js
T = db.model('T', new Schema({ x: { type: String, select: true }}));
T.find(..); // field x will always be selected ..
// .. unless overridden;
T.find().select('-x').exec(callback);
```

<!--sec data-title="源码" data-id="SchemaType_select" data-show=true data-collapse=true ces-->
```js
SchemaType.prototype.select = function select(val) {
  this.selected = !!val;
  return this;
};
```
<!--endsec-->


## SchemaType#set(fn)

Adds a setter to this schematype.

##### 参数：

  * `fn` &lt;[Function][]&gt;

##### 返回值：

  * <SchemaType> this

##### 示例：

```js
function capitalize (val) {
  if (typeof val !== 'string') val = '';
  return val.charAt(0).toUpperCase() + val.substring(1);
}

// defining within the schema
var s = new Schema({ name: { type: String, set: capitalize }})

// or by retreiving its SchemaType
var s = new Schema({ name: String })
s.path('name').set(capitalize)
```
Setters allow you to transform the data before it gets to the raw mongodb document and is set as a value on an actual key.

Suppose you are implementing user registration for a website. Users provide an email and password, which gets saved to mongodb. The email is a string that you will want to normalize to lower case, in order to avoid one email having more than one account -- e.g., otherwise, avenue@q.com can be registered for 2 accounts via avenue@q.com and AvEnUe@Q.CoM.

You can set up email lower case normalization easily via a Mongoose setter.

```js
function toLower(v) {
  return v.toLowerCase();
}

var UserSchema = new Schema({
  email: { type: String, set: toLower }
});

var User = db.model('User', UserSchema);

var user = new User({email: 'AVENUE@Q.COM'});
console.log(user.email); // 'avenue@q.com'

// or
var user = new User();
user.email = 'Avenue@Q.com';
console.log(user.email); // 'avenue@q.com'
```

As you can see above, setters allow you to transform the data before it stored in MongoDB.

##### 注意：

setters by default do not run on queries by default.

// Will **not** run the `toLower()` setter by default.
User.updateOne({ _id: _id }, { $set: { email: 'AVENUE@Q.COM' } });
Use the runSettersOnQuery option to opt-in to running setters on User.update():

// Turn on `runSettersOnQuery` to run the setters from your schema.
User.updateOne({ _id: _id }, { $set: { email: 'AVENUE@Q.COM' } }, {
  runSettersOnQuery: true
});
##### 注意：

we could have also just used the built-in lowercase: true SchemaType option instead of defining our own function.

```js
new Schema({ email: { type: String, lowercase: true }})
Setters are also passed a second argument, the schematype on which the setter was defined. This allows for tailored behavior based on options passed in the schema.

function inspector (val, schematype) {
  if (schematype.options.required) {
    return schematype.path + ' is required';
  } else {
    return val;
  }
}

var VirusSchema = new Schema({
  name: { type: String, required: true, set: inspector },
  taxonomy: { type: String, set: inspector }
})

var Virus = db.model('Virus', VirusSchema);
var v = new Virus({ name: 'Parvoviridae', taxonomy: 'Parvovirinae' });

console.log(v.name);     // name is required
console.log(v.taxonomy); // Parvovirinae
```

<!--sec data-title="源码" data-id="SchemaType_set" data-show=true data-collapse=true ces-->
```js
SchemaType.prototype.set = function(fn) {
  if (typeof fn !== 'function') {
    throw new TypeError('A setter must be a function.');
  }
  this.setters.push(fn);
  return this;
};
```
<!--endsec-->


## SchemaType#sparse(bool)

Declares a sparse index.

##### 参数：

  * `bool` &lt;[Boolean][]&gt;

##### 返回值：

  * <SchemaType> this

##### 示例：

```js
var s = new Schema({ name: { type: String, sparse: true }})
Schema.path('name').index({ sparse: true });
```

<!--sec data-title="源码" data-id="SchemaType_sparse" data-show=true data-collapse=true ces-->
```js
SchemaType.prototype.sparse = function(bool) {
  if (this._index === null || this._index === undefined ||
    typeof this._index === 'boolean') {
    this._index = {};
  } else if (typeof this._index === 'string') {
    this._index = {type: this._index};
  }

  this._index.sparse = bool;
  return this;
};
```
<!--endsec-->



## SchemaType#text(bool)


Declares a full text index.

##### 参数：

  * `bool` &lt;[Boolean][]&gt;

##### 返回值：

  * <SchemaType> this

##### 示例：

```js
var s = new Schema({name : {type: String, text : true }})
 Schema.path('name').index({text : true});
```

<!--sec data-title="源码" data-id="SchemaType_text" data-show=true data-collapse=true ces-->
```js
SchemaType.prototype.text = function(bool) {
  if (this._index === null || this._index === undefined ||
    typeof this._index === 'boolean') {
    this._index = {};
  } else if (typeof this._index === 'string') {
    this._index = {type: this._index};
  }

  this._index.text = bool;
  return this;
};
```
<!--endsec-->


## SchemaType#unique(bool)

Declares an unique index.

##### 参数：

  * `bool` &lt;[Boolean][]&gt;

##### 返回值：

  * <SchemaType> this

##### 示例：

```js
var s = new Schema({ name: { type: String, unique: true }});
Schema.path('name').index({ unique: true });
```

##### 注意：

violating the constraint returns an E11000 error from MongoDB when saving, not a Mongoose validation error.

<!--sec data-title="源码" data-id="SchemaType_unique" data-show=true data-collapse=true ces-->
```js
SchemaType.prototype.unique = function(bool) {
  if (this._index === false) {
    if (!bool) {
      return;
    }
    throw new Error('Path "' + this.path + '" may not have `index` set to ' +
      'false and `unique` set to true');
  }
  if (this._index == null || this._index === true) {
    this._index = {};
  } else if (typeof this._index === 'string') {
    this._index = {type: this._index};
  }

  this._index.unique = bool;
  return this;
};
```
<!--endsec-->


## SchemaType#validate(obj, [errorMsg], [type])

Adds validator(s) for this document path.

##### 参数：

  * `obj` <RegExp, Function, Object> validator

  * `[errorMsg]` &lt;[String][]&gt; optional error message

  * `[type]` &lt;[String][]&gt; optional validator type

##### 返回值：

  * <SchemaType> this

Validators always receive the value to validate as their first argument and must return Boolean. Returning false means validation failed.

The error message argument is optional. If not passed, the default generic error message template will be used.

##### 示例：

```js
// make sure every value is equal to "something"
function validator (val) {
  return val == 'something';
}
new Schema({ name: { type: String, validate: validator }});

// with a custom error message

var custom = [validator, 'Uh oh, {PATH} does not equal "something".']
new Schema({ name: { type: String, validate: custom }});

// adding many validators at a time

var many = [
    { validator: validator, msg: 'uh oh' }
  , { validator: anotherValidator, msg: 'failed' }
]
new Schema({ name: { type: String, validate: many }});

// or utilizing SchemaType methods directly:

var schema = new Schema({ name: 'string' });
schema.path('name').validate(validator, 'validation of `{PATH}` failed with value `{VALUE}`');
```

##### Error message templates:
From the examples above, you may have noticed that error messages support basic templating. There are a few other template keywords besides {PATH} and {VALUE} too. To find out more, details are available here

##### Asynchronous validation:

Passing a validator function that receives two arguments tells mongoose that the validator is an asynchronous validator. The first argument passed to the validator function is the value being validated. The second argument is a callback function that must called when you finish validating the value and passed either true or false to communicate either success or failure respectively.

```js
schema.path('name').validate({
  isAsync: true,
  validator: function (value, respond) {
    doStuff(value, function () {
      ...
      respond(false); // validation failed
    });
  },
  message: 'Custom error message!' // Optional
});

// Can also return a promise
schema.path('name').validate({
  validator: function (value) {
    return new Promise(function (resolve, reject) {
      resolve(false); // validation failed
    });
  }
});
```

You might use asynchronous validators to retreive other documents from the database to validate against or to meet other I/O bound validation needs.

Validation occurs pre('save') or whenever you manually execute document#validate.

If validation fails during pre('save') and no callback was passed to receive the error, an error event will be emitted on your Models associated db connection, passing the validation error object along.

```js
var conn = mongoose.createConnection(..);
conn.on('error', handleError);

var Product = conn.model('Product', yourSchema);
var dvd = new Product(..);
dvd.save(); // emits error on the `conn` above
```

If you desire handling these errors at the Model level, attach an error listener to your Model and the event will instead be emitted there.

```js
// registering an error listener on the Model lets us handle errors more locally
Product.on('error', handleError);
```

<!--sec data-title="源码" data-id="SchemaType_validate" data-show=true data-collapse=true ces-->
```js
SchemaType.prototype.validate = function(obj, message, type) {
  if (typeof obj === 'function' || obj && utils.getFunctionName(obj.constructor) === 'RegExp') {
    var properties;
    if (message instanceof Object && !type) {
      properties = utils.clone(message);
      if (!properties.message) {
        properties.message = properties.msg;
      }
      properties.validator = obj;
      properties.type = properties.type || 'user defined';
    } else {
      if (!message) {
        message = MongooseError.messages.general.default;
      }
      if (!type) {
        type = 'user defined';
      }
      properties = {message: message, type: type, validator: obj};
    }
    this.validators.push(properties);
    return this;
  }

  var i,
      length,
      arg;

  for (i = 0, length = arguments.length; i < length; i++) {
    arg = arguments[i];
    if (!(arg && utils.getFunctionName(arg.constructor) === 'Object')) {
      var msg = 'Invalid validator. Received (' + typeof arg + ') '
          + arg
          + '. See http://mongoosejs.com/docs/api.html#schematype_SchemaType-validate';

      throw new Error(msg);
    }
    this.validate(arg.validator, arg);
  }

  return this;
};

```
<!--endsec-->

----


# connection.js

> 源码：[connection.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/connection.js)


## Connection#close([force], [callback])

Closes the connection

##### 参数：

  * [force] &lt;[Boolean][]&gt; optional

  * [callback] &lt;[Function][]&gt; optional

##### 返回值：

  * <Connection> self

<!--sec data-title="源码" data-id="Connection_close" data-show=true data-collapse=true ces-->
```js
Connection.prototype.close = function(force, callback) {
  var _this = this;
  var Promise = PromiseProvider.get();

  if (typeof force === 'function') {
    callback = force;
    force = false;
  }

  this.$wasForceClosed = !!force;

  return new Promise.ES6(function(resolve, reject) {
    _this._close(force, function(error) {
      callback && callback(error);
      if (error) {
        reject(error);
        return;
      }
      resolve();
    });
  });
};
```
<!--endsec-->

## Connection#collection(name, [options])

Retrieves a collection, creating it if not cached.

##### 参数：

  * `name` &lt;[String][]&gt; of the collection

  * `[options]` &lt;[Object][]&gt; optional collection options

##### 返回值：

  * <Collection> collection instance

Not typically needed by applications. Just talk to your collection through your model.

<!--sec data-title="源码" data-id="Connection_collection" data-show=true data-collapse=true ces-->
```js
Connection.prototype.collection = function(name, options) {
  options = options ? utils.clone(options, { retainKeyOrder: true }) : {};
  options.$wasForceClosed = this.$wasForceClosed;
  if (!(name in this.collections)) {
    this.collections[name] = new Collection(name, this, options);
  }
  return this.collections[name];
};
```
<!--endsec-->


## Connection(base)

Connection constructor

##### 参数：

  * base <[Mongoose]()> a mongoose instance

##### 继承：

  * [NodeJS EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)

##### 事件：

  * `connecting`: Emitted when connection.{open,openSet}() is executed on this connection.

  * `connected`: Emitted when this connection successfully connects to the db. May be emitted multiple times in reconnected scenarios.

  * `open`: Emitted after we connected and onOpen is executed on all of this connections models.

  * `disconnecting`: Emitted when connection.close() was executed.

  * `disconnected`: Emitted after getting disconnected from the db.

  * `close`: Emitted after we disconnected and onClose executed on all of this connections models.

  * `reconnected`: Emitted after we connected and subsequently disconnected, followed by successfully another successfull connection.

  * `error`: Emitted when an error occurs on this connection.

  * `fullsetup`: Emitted in a replica-set scenario, when primary and at least one seconaries specified in the connection string are connected.

  * `all`: Emitted in a replica-set scenario, when all nodes specified in the connection string are connected.

For practical reasons, a Connection equals a Db.

<!--sec data-title="源码" data-id="Connection" data-show=true data-collapse=true ces-->
```js
function Connection(base) {
  this.base = base;
  this.collections = {};
  this.models = {};
  this.config = {autoIndex: true};
  this.replica = false;
  this.hosts = null;
  this.host = null;
  this.port = null;
  this.user = null;
  this.pass = null;
  this.name = null;
  this.options = null;
  this.otherDbs = [];
  this.states = STATES;
  this._readyState = STATES.disconnected;
  this._closeCalled = false;
  this._hasOpened = false;
}
```
<!--endsec-->


## (collection, [options], [callback])

Helper for createCollection(). Will explicitly create the given collection
with specified options. Used to create capped collections
and views from mongoose.

##### 参数：

  * `collection` &lt;[String][]&gt; The collection to delete

  * `[options]` &lt;[Object][]&gt; see MongoDB driver docs

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <[Promise]()>

Options are passed down without modification to the [MongoDB driver's createCollection() function](http://mongodb.github.io/node-mongodb-native/2.2/api/Db.html#createCollection)

<!--sec data-title="源码" data-id="12" data-show=true data-collapse=true ces-->
```js
Connection.prototype.createCollection = _wrapConnHelper(function createCollection(collection, options, cb) {
  if (typeof options === 'function') {
    cb = options;
    options = {};
  }
  this.db.createCollection(collection, options, cb);
});
```
<!--endsec-->


## (collection, [callback])

Helper for dropCollection(). Will delete the given collection, including
all documents and indexes.

##### 参数：

  * `collection` &lt;[String][]&gt; The collection to delete

  * `[callback]` &lt;[Function][]&gt;

##### 返回值：

  * <[Promise]()>


<!--sec data-title="源码" data-id="13" data-show=true data-collapse=true ces-->
```js
Connection.prototype.dropCollection = _wrapConnHelper(function dropCollection(collection, cb) {
  this.db.dropCollection(collection, cb);
});
```
<!--endsec-->

## ([callback])

Helper for dropDatabase(). Deletes the given database, including all
collections, documents, and indexes.

##### 参数：
[callback] &lt;[Function][]&gt;
##### 返回值：
<Promise>
<!--sec data-title="源码" data-id="14" data-show=true data-collapse=true ces-->
```js
Connection.prototype.dropDatabase = _wrapConnHelper(function dropDatabase(cb) {
  this.db.dropDatabase(cb);
});
```
<!--endsec-->

## Connection#model(name, [schema], [collection])

Defines or retrieves a model.

##### 参数：

  * `name` &lt;[String][]&gt; the model name

  * `[schema]` <Schema> a schema. necessary when defining a model

  * `[collection]` &lt;[String][]&gt; name of mongodb collection (optional) if not given it will be induced from model name

##### 返回值：

  * <Model> The compiled model

##### 参见：

  * [Mongoose#model]()

```js
var mongoose = require('mongoose');
var db = mongoose.createConnection(..);
db.model('Venue', new Schema(..));
var Ticket = db.model('Ticket', new Schema(..));
var Venue = db.model('Venue');
```

When no collection argument is passed, Mongoose produces a collection name by passing the model name to the [utils.toCollectionName](http://mongoosejs.com/docs/api.html#utils_exports.toCollectionName) method. This method pluralizes the name. If you don't like this behavior, either pass a collection name or set your schemas collection name option.

##### 示例：

```js
var schema = new Schema({ name: String }, { collection: 'actor' });

// or

schema.set('collection', 'actor');

// or

var collectionName = 'actor'
var M = conn.model('Actor', schema, collectionName)
```

<!--sec data-title="源码" data-id="Connection_model" data-show=true data-collapse=true ces-->
```js
Connection.prototype.model = function(name, schema, collection) {
  // collection name discovery
  if (typeof schema === 'string') {
    collection = schema;
    schema = false;
  }

  if (utils.isObject(schema) && !schema.instanceOfSchema) {
    schema = new Schema(schema);
  }
  if (schema && !schema.instanceOfSchema) {
    throw new Error('The 2nd parameter to `mongoose.model()` should be a ' +
      'schema or a POJO');
  }

  if (this.models[name] && !collection) {
    // model exists but we are not subclassing with custom collection
    if (schema && schema.instanceOfSchema && schema !== this.models[name].schema) {
      throw new MongooseError.OverwriteModelError(name);
    }
    return this.models[name];
  }

  var opts = {cache: false, connection: this};
  var model;

  if (schema && schema.instanceOfSchema) {
    // compile a model
    model = this.base.model(name, schema, collection, opts);

    // only the first model with this name is cached to allow
    // for one-offs with custom collection names etc.
    if (!this.models[name]) {
      this.models[name] = model;
    }

    model.init();
    return model;
  }

  if (this.models[name] && collection) {
    // subclassing current model with alternate collection
    model = this.models[name];
    schema = model.prototype.schema;
    var sub = model.__subclass(this, schema, collection);
    // do not cache the sub model
    return sub;
  }

  // lookup model in mongoose module
  model = this.base.models[name];

  if (!model) {
    throw new MongooseError.MissingSchemaError(name);
  }

  if (this === model.prototype.db
      && (!collection || collection === model.collection.name)) {
    // model already uses this connection.

    // only the first model with this name is cached to allow
    // for one-offs with custom collection names etc.
    if (!this.models[name]) {
      this.models[name] = model;
    }

    return model;
  }
  this.models[name] = model.__subclass(this, schema, collection);
  return this.models[name];
};
```
<!--endsec-->

## Connection#modelNames()

Returns an array of model names created on this connection.

##### 返回值：
&lt;[Array][]&gt;
<!--sec data-title="源码" data-id="Connection_modelNames" data-show=true data-collapse=true ces-->
```js
```
<!--endsec-->

## (connection_string, [database], [port], [options], [callback])

Opens the connection to MongoDB.

##### 参数：

  * `connection_string` &lt;[String][]&gt; mongodb://uri or the host to which you are connecting
  * `[database]` &lt;[String][]&gt; database name
  * `[port]` <Number> database port
  * `[options]` &lt;[Object][]&gt; options
  * `[callback]` &lt;[Function][]&gt;


##### 参见：

  * node-mongodb-native
  *
  * http://mongodb.github.com/node-mongodb-native/api-generated/db.html#authenticate


options is a hash with the following possible properties:

<pre>
config  - passed to the connection config instance
db      - passed to the connection db instance
server  - passed to the connection server instance(s)
replset - passed to the connection ReplSet instance
user    - username for authentication
pass    - password for authentication
auth    - options for authentication (see http://mongodb.github.com/node-mongodb-native/api-generated/db.html#authenticate)
</pre>

##### 示例：

Mongoose forces the db option forceServerObjectId false and cannot be overridden.
Mongoose defaults the server auto_reconnect options to true which can be overridden.
See the node-mongodb-native driver instance for options that it understands.

*Options passed take precedence over options included in connection strings.*

<!--sec data-title="源码" data-id="14" data-show=true data-collapse=true ces-->
```js
Connection.prototype.open = util.deprecate(function() {
  var Promise = PromiseProvider.get();
  var callback;

  try {
    callback = this._handleOpenArgs.apply(this, arguments);
  } catch (error) {
    return new Promise.ES6(function(resolve, reject) {
      reject(error);
    });
  }

  var _this = this;
  var promise = new Promise.ES6(function(resolve, reject) {
    _this._open(true, function(error) {
      callback && callback(error);
      if (error) {
        // Error can be on same tick re: christkv/mongodb-core#157
        setImmediate(function() {
          reject(error);
          if (!callback && !promise.$hasHandler) {
            _this.emit('error', error);
          }
        });
        return;
      }
      resolve();
    });
  });

  // Monkey-patch `.then()` so if the promise is handled, we don't emit an
  // `error` event.
  var _then = promise.then;
  promise.then = function(resolve, reject) {
    promise.$hasHandler = true;
    return _then.call(promise, resolve, reject);
  };

  return promise;
}, '`open()` is deprecated in mongoose >= 4.11.0, use `openUri()` instead, or set the `useMongoClient` option if using `connect()` or `createConnection()`. See http://mongoosejs.com/docs/connections.html#use-mongo-client');
```
<!--endsec-->

## (uris, [database], [options], [callback])

Opens the connection to a replica set.

##### 参数：

  * `uris` &lt;[String][]&gt; MongoDB connection string

  * `[database]` &lt;[String][]&gt; database name if not included in uris

  * `[options]` &lt;[Object][]&gt; passed to the internal driver

  * `[callback]` &lt;[Function][]&gt;

##### 参见：

  * [node-mongodb-native](https://github.com/mongodb/node-mongodb-native)
  * http://mongodb.github.com/node-mongodb-native/api-generated/db.html#authenticate

##### 示例：

```js
var db = mongoose.createConnection();
db.openSet("mongodb://user:pwd@localhost:27020,localhost:27021,localhost:27012/mydb");
```

The database name and/or auth need only be included in one URI.
The options is a hash which is passed to the internal driver connection object.

Valid options

<pre>
db      - passed to the connection db instance
server  - passed to the connection server instance(s)
replset - passed to the connection ReplSetServer instance
user    - username for authentication
pass    - password for authentication
auth    - options for authentication (see http://mongodb.github.com/node-mongodb-native/api-generated/db.html#authenticate)
mongos  - Boolean - if true, enables High Availability support for mongos
</pre>

*Options passed take precedence over options included in connection strings.*


##### 注意：

*If connecting to multiple mongos servers, set the mongos option to true.*

```js
conn.open('mongodb://mongosA:27501,mongosB:27501', { mongos: true }, cb);
```

Mongoose forces the db option forceServerObjectId false and cannot be overridden.
Mongoose defaults the server auto_reconnect options to true which can be overridden.
See the node-mongodb-native driver instance for options that it understands.

*Options passed take precedence over options included in connection strings.*

<!--sec data-title="源码" data-id="15" data-show=true data-collapse=true ces-->
```js
Connection.prototype.openSet = util.deprecate(function(uris, database, options, callback) {
  var Promise = PromiseProvider.get();

  try {
    callback = this._handleOpenSetArgs.apply(this, arguments);
  } catch (err) {
    return new Promise.ES6(function(resolve, reject) {
      reject(err);
    });
  }

  var _this = this;
  var emitted = false;
  var promise = new Promise.ES6(function(resolve, reject) {
    _this._open(true, function(error) {
      callback && callback(error);
      if (error) {
        reject(error);
        if (!callback && !promise.$hasHandler && !emitted) {
          emitted = true;
          _this.emit('error', error);
        }
        return;
      }
      resolve();
    });
  });

  // Monkey-patch `.then()` so if the promise is handled, we don't emit an
  // `error` event.
  var _then = promise.then;
  promise.then = function(resolve, reject) {
    promise.$hasHandler = true;
    return _then.call(promise, resolve, reject);
  };

  return promise;
}, '`openSet()` is deprecated in mongoose >= 4.11.0, use `openUri()` instead, or set the `useMongoClient` option if using `connect()` or `createConnection()`. See http://mongoosejs.com/docs/connections.html#use-mongo-client');
```
<!--endsec-->

## Connection#collections

A hash of the collections associated with this connection

<!--sec data-title="源码" data-id="Connection_collections" data-show=true data-collapse=true ces-->
```js
Connection.prototype.collections;
```
<!--endsec-->

## Connection#config

A hash of the global options that are associated with this connection

<!--sec data-title="源码" data-id="Connection_config" data-show=true data-collapse=true ces-->
```js
Connection.prototype.config;
```
<!--endsec-->

## Connection#db

The mongodb.Db instance, set when the connection is opened

<!--sec data-title="源码" data-id="Connection_db" data-show=true data-collapse=true ces-->
```js
Connection.prototype.db;
```
<!--endsec-->

## Connection#readyState

Connection ready state

  * 0 = disconnected
  * 1 = connected
  * 2 = connecting
  * 3 = disconnecting


Each state change emits its associated event name.

##### 示例：

```js
conn.on('connected', callback);
conn.on('disconnected', callback);
```

<!--sec data-title="源码" data-id="Connection_readyState" data-show=true data-collapse=true ces-->
```js
Object.defineProperty(Connection.prototype, 'readyState', {
  get: function() {
    return this._readyState;
  },
  set: function(val) {
    if (!(val in STATES)) {
      throw new Error('Invalid connection state: ' + val);
    }

    if (this._readyState !== val) {
      this._readyState = val;
      // loop over the otherDbs on this connection and change their state
      for (var i = 0; i < this.otherDbs.length; i++) {
        this.otherDbs[i].readyState = val;
      }

      if (STATES.connected === val) {
        this._hasOpened = true;
      }

      this.emit(STATES[val]);
    }
  }
});
```
<!--endsec-->

----

# collection.js

> 源码：[collection.js](https://github.com/Automattic/mongoose/blob/4.13.7/lib/collection.js)


## Collection(name, conn, opts)

Abstract Collection constructor

##### 参数：

  ** `name` &lt;[String][]&gt; name of the collection

  ** `conn` <Connection> A MongooseConnection instance

  ** `opts` &lt;[Object][]&gt; optional collection options

This is the base class that drivers inherit from and implement.


<!--sec data-title="源码" data-id="16" data-show=true data-collapse=true ces-->
```js
function Collection(name, conn, opts) {
  if (opts === void 0) {
    opts = {};
  }
  if (opts.capped === void 0) {
    opts.capped = {};
  }

  opts.bufferCommands = undefined === opts.bufferCommands
      ? true
      : opts.bufferCommands;

  if (typeof opts.capped === 'number') {
    opts.capped = {size: opts.capped};
  }

  this.opts = opts;
  this.name = name;
  this.collectionName = name;
  this.conn = conn;
  this.queue = [];
  this.buffer = this.opts.bufferCommands;
  this.emitter = new EventEmitter();

  if (STATES.connected === this.conn.readyState) {
    this.onOpen();
  }
}
```
<!--endsec-->

## Collection#createIndex()

Abstract method that drivers must implement.

<!--sec data-title="源码" data-id="Collection_createIndex" data-show=true data-collapse=true ces-->
```js
Collection.prototype.createIndex = function() {
  throw new Error('Collection#ensureIndex unimplemented by driver');
};
```
<!--endsec-->

## Collection#ensureIndex()

Abstract method that drivers must implement.

<!--sec data-title="源码" data-id="Collection_ensureIndex" data-show=true data-collapse=true ces-->
```js
Collection.prototype.ensureIndex = function() {
  throw new Error('Collection#ensureIndex unimplemented by driver');
};
```
<!--endsec-->

## Collection#find()

Abstract method that drivers must implement.

<!--sec data-title="源码" data-id="Collection_find" data-show=true data-collapse=true ces-->
```js
Collection.prototype.find = function() {
  throw new Error('Collection#find unimplemented by driver');
};
```
<!--endsec-->

## Collection#findAndModify()

Abstract method that drivers must implement.

<!--sec data-title="源码" data-id="Collection_findAndModify" data-show=true data-collapse=true ces-->
```js
Collection.prototype.findAndModify = function() {
  throw new Error('Collection#findAndModify unimplemented by driver');
};
```
<!--endsec-->

## Collection#findOne()

Abstract method that drivers must implement.

<!--sec data-title="源码" data-id="Collection_findOne" data-show=true data-collapse=true ces-->
```js
Collection.prototype.findOne = function() {
  throw new Error('Collection#findOne unimplemented by driver');
};
```
<!--endsec-->

## Collection#getIndexes()

Abstract method that drivers must implement.

<!--sec data-title="源码" data-id="Collection_getIndexes" data-show=true data-collapse=true ces-->
```js
Collection.prototype.getIndexes = function() {
  throw new Error('Collection#getIndexes unimplemented by driver');
};
```
<!--endsec-->

## Collection#insert()

Abstract method that drivers must implement.

<!--sec data-title="源码" data-id="Collection_insert" data-show=true data-collapse=true ces-->
```js
Collection.prototype.insert = function() {
  throw new Error('Collection#insert unimplemented by driver');
};
```
<!--endsec-->

## Collection#mapReduce()

Abstract method that drivers must implement.

<!--sec data-title="源码" data-id="Collection_mapReduce" data-show=true data-collapse=true ces-->
```js
Collection.prototype.mapReduce = function() {
  throw new Error('Collection#mapReduce unimplemented by driver');
};
```
<!--endsec-->

## Collection#save()

Abstract method that drivers must implement.

<!--sec data-title="源码" data-id="Collection_save" data-show=true data-collapse=true ces-->
```js
Collection.prototype.save = function() {
  throw new Error('Collection#save unimplemented by driver');
};
```
<!--endsec-->

## Collection#update()

Abstract method that drivers must implement.

<!--sec data-title="源码" data-id="Collection_update" data-show=true data-collapse=true ces-->
```js
Collection.prototype.update = function() {
  throw new Error('Collection#update unimplemented by driver');
};
```
<!--endsec-->

## Collection#collectionName

The collection name

<!--sec data-title="源码" data-id="Collection_collectionName" data-show=true data-collapse=true ces-->
```js
Collection.prototype.collectionName;
```
<!--endsec-->

## Collection#conn

The Connection instance

<!--sec data-title="源码" data-id="Collection_conn" data-show=true data-collapse=true ces-->
```js
Collection.prototype.conn;
```
<!--endsec-->

## Collection#name

The collection name

<!--sec data-title="源码" data-id="Collection_name" data-show=true data-collapse=true ces-->
```js
Collection.prototype.name;
```
<!--endsec-->

[String]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String
[Array]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array
[Error]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Error
[Object]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object
[Function]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function
[Boolean]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Boolean


[Any]: #Any
[MongooseThenable]: #MongooseThenable
