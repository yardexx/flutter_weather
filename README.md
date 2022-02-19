# flutter_weather

Weather application
from [bloclibrary.dev tutorial](https://bloclibrary.dev/#/flutterweathertutorial)
with custom comments and notes for practical and explanation reasons.

## Getting Started

* Clone repository
* cd to your local project
* `flutter run` in terminal or run manually in your IDE

## Tips & tricks

### Different layers

Application has different packages which essentially divides logic of application. Each of these
packages can be used independently/can be replaced with other with minor changes in code.

Data layer gets (meta_weather_api package) gets us raw data. Repository layer get and formats data
from data layer. Repository layer doesn't care how are data retrieved, it only cares about data
it's.

Same logic applies in business logic. Business logic doesn't care from which source repository has
retrieved data. It just shows data it got from it and/or asks for new data.

### Adding another (internal) Dart package

Dart package can be created using
`dart create --template=package-simple name_of_package`
so that we don't have to remove all (in this case unnecessary) Flutter dependencies.

### TLDR; on JSON serializing

For JSON serializing using `json_serializable` package we have to

* annotate our model class (
  see [weather.dart](packages/weather_repository/lib/src/models/weather.dart))
* add [build.yaml](packages/weather_repository/build.yaml) to corresponding (sub)project
* run `flutter packages pub run build_runner build` command in (sub)project

More info how to annotate for [JSON_serializable](https://pub.dev/packages/json_serializable) and
about [build_runner](https://pub.dev/packages/build_runner)

### Unclear syntax comments

```dart
class WeatherRepository {
  WeatherRepository({MetaWeatherApiClient? weatherApiClient})
      : _weatherApiClient = weatherApiClient ?? MetaWeatherApiClient();
}
```

WeatherRepository takes one parameter in constructor - object of MetaWeatherApiClient type which **
can be null**. Part after `:` is checking whether provided parameter is null. If not, use it to
construct object. If it is null, create new ("default") instance of MetaWeatherApiClient and use it.