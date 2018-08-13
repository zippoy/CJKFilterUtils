# CJKFilterUtils

[![Build Status](https://travis-ci.org/sul-dlss/CJKFilterUtils.svg?branch=master)](https://travis-ci.org/sul-dlss/CJKFilterUtils) [![codecov](https://codecov.io/gh/sul-dlss/CJKFilterUtils/branch/master/graph/badge.svg)](https://codecov.io/gh/sul-dlss/CJKFilterUtils)


This is a Lucene filter and filter factory (see http://lucene.apache.org )
to fold certain CJK characters to improve recall.  You should put it in your
analysis chain BEFORE ICUTransforms from Traditional->Simplified Han, as it
converts modern Japanese Kanji to their traditional equivalents.

## Usage

- clone the project

 git clone git://github.com/solrmarc/CJKFilterUtils.git

- run the maven installation

 maven clean install

- put the `CJKFilterUtils*.jar` file found in the target directory into your Solr lib directory
- utilize the Solr CJKFoldingFilterFactory in your schema.xml file.

 <fieldType name="text_cjk" class="solr.TextField" positionIncrementGap="10000" autoGeneratePhraseQueries="false">
   <analyzer>
     <tokenizer class="solr.ICUTokenizerFactory" />
     <filter class="solr.CJKWidthFilterFactory"/>
     <filter class="edu.stanford.lucene.analysis.CJKFoldingFilterFactory"/>
     <filter class="solr.ICUTransformFilterFactory" id="Traditional-Simplified"/>
     <filter class="solr.ICUTransformFilterFactory" id="Katakana-Hiragana"/>
     <filter class="solr.ICUFoldingFilterFactory"/>
     <filter class="solr.CJKBigramFilterFactory" han="true" hiragana="true" katakana="true" hangul="true" outputUnigrams="true" />
   </analyzer>
 </fieldType>

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request