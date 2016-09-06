# Complex Logic Assessment

<script>

  var assessment = new Assessment()
  var results = new Results()

  var locationSurvey = DocLoader('location-suvey')
  var gridTest = DocLoader('grid-test')
  var readingComprehension = DocLoader('reading-comprehension')

  // Focus on first document.
  assessment.focus(locationSurvey)

  assessment.on('document:done', function(doneDocument, result) {

    results.add(result)

    if (results.length == 1) {
      assessment.focus(gridTest)
      gridTest.on('document:done', function() { assessment.trigger('documentDone:done') })
    }

    if (results.length == 2 && result.score > 72) {
      assessment.play(readingComprehension)
      readingComprehension.on('document:done', function() { assessment.trigger('document:done')})
    }
    else {
       assessment.trigger('assessment:done')
    }

    if (doneItem.id == readingComprehension.id) {
      assessment.trigger('assessment:done')
    }

  })

</script>
